# Código Fuente

```python
import time
import threading
from datetime import datetime

import RPi.GPIO as GPIO
from flask import Flask, send_file

# Pines físicos de la Raspberry Pi (numeración BOARD)
PIR_PIN = 11       # Salida del sensor PIR
LED_PIN = 12       # LED mediante resistencia de 220 ohmios
TRIG_PIN = 16      # Trigger del sensor ultrasónico
ECHO_PIN = 18      # Echo del sensor ultrasónico mediante divisor de tensión

# Parámetros del sistema
DISTANCIA_MAXIMA_CM = 150
TIEMPO_ACTIVACION_S = 5
TIEMPO_REPOSO_S = 8
TIEMPO_REARME_S = 1
INTERVALO_BEACON_S = 5
MAX_EVENTOS = 30
FOTO_PATH = "/tmp/agrosafe_ultima.jpg"

# Inicialización opcional de la cámara
camara = None

try:
    from picamera2 import Picamera2

    camara = Picamera2()
    camara.configure(camara.create_still_configuration())
    camara.start()
    print("Cámara detectada.")

except Exception as e:
    camara = None
    print(f"Sin cámara: el sistema funciona igual. Detalle: {e}")


def tomar_foto():
    """Toma una fotografía si la cámara está disponible."""
    if camara is None:
        return False

    try:
        camara.capture_file(FOTO_PATH)
        return True

    except Exception as e:
        print("Error al tomar foto:", e)
        return False


# Configuración de GPIO
GPIO.setwarnings(False)
GPIO.setmode(GPIO.BOARD)
GPIO.setup(PIR_PIN, GPIO.IN)
GPIO.setup(LED_PIN, GPIO.OUT, initial=GPIO.LOW)
GPIO.setup(TRIG_PIN, GPIO.OUT, initial=GPIO.LOW)
GPIO.setup(ECHO_PIN, GPIO.IN)


def medir_distancia_cm():
    """Mide la distancia con el HC-SR04. Devuelve -1 si no hay eco."""
    GPIO.output(TRIG_PIN, GPIO.HIGH)
    time.sleep(0.00001)
    GPIO.output(TRIG_PIN, GPIO.LOW)

    limite = time.monotonic() + 0.05
    inicio = time.monotonic()

    while GPIO.input(ECHO_PIN) == 0:
        inicio = time.monotonic()

        if inicio > limite:
            return -1

    fin = time.monotonic()

    while GPIO.input(ECHO_PIN) == 1:
        fin = time.monotonic()

        if fin > limite + 0.05:
            return -1

    return round((fin - inicio) * 34300 / 2, 1)


# Registro de eventos
eventos = []
lock = threading.Lock()


def registrar(estado, distancia, foto=False):
    """Registra un evento con su hora, distancia y estado."""
    evento = {
        "hora": datetime.now().strftime("%H:%M:%S"),
        "estado": estado,
        "distancia": distancia,
        "foto": foto,
    }

    with lock:
        eventos.insert(0, evento)
        del eventos[MAX_EVENTOS:]

    print(evento)


# Lógica principal: sensores y actuador de prueba
def bucle_sensores():
    ultimo_beacon = 0
    preparado = False
    inactivo_desde = None

    while True:
        ahora = time.monotonic()

        if ahora - ultimo_beacon >= INTERVALO_BEACON_S:
            registrar("reposo", medir_distancia_cm())
            ultimo_beacon = ahora

        movimiento = bool(GPIO.input(PIR_PIN))

        if not movimiento:
            if inactivo_desde is None:
                inactivo_desde = time.monotonic()

            elif time.monotonic() - inactivo_desde >= TIEMPO_REARME_S:
                preparado = True

        else:
            inactivo_desde = None

        if movimiento and preparado:
            # Consumir la detección para evitar activaciones repetidas
            # mientras la señal del PIR permanezca activa.
            preparado = False
            distancia = medir_distancia_cm()

            if 0 < distancia < DISTANCIA_MAXIMA_CM:
                GPIO.output(LED_PIN, GPIO.HIGH)

                try:
                    foto = tomar_foto()
                    registrar("activado", distancia, foto)
                    time.sleep(TIEMPO_ACTIVACION_S)

                finally:
                    GPIO.output(LED_PIN, GPIO.LOW)

                time.sleep(TIEMPO_REPOSO_S)

            else:
                registrar("descartado", distancia)
                time.sleep(1)

        time.sleep(0.1)


# Aplicación web con Flask
app = Flask(__name__)

COLORES = {
    "activado": "#e74c3c",
    "descartado": "#f39c12",
    "reposo": "#27ae60",
}


@app.route("/")
def dashboard():
    with lock:
        lista = list(eventos)

    ultimo = lista[0] if lista else None

    filas = ""

    for evento in lista:
        color = COLORES.get(evento["estado"], "#888")

        filas += (
            f"<tr><td>{evento['hora']}</td>"
            f"<td style='color:{color};font-weight:bold'>"
            f"{evento['estado']}</td>"
            f"<td>{evento['distancia']} cm</td></tr>"
        )

    estado_html = "Esperando datos..."

    if ultimo:
        color = COLORES.get(ultimo["estado"], "#888")

        estado_html = (
            f"<span style='color:{color}'>"
            f"{ultimo['estado'].upper()}</span>"
            f" &middot; {ultimo['distancia']} cm"
            f" &middot; {ultimo['hora']}"
        )

    foto_html = ""

    if camara is not None:
        foto_html = (
            "<h2>Última foto</h2>"
            f"<img src='/foto?t={time.time()}' style='max-width:100%'>"
        )

    return f"""<!doctype html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta http-equiv="refresh" content="2">
<title>AGROSAFE</title>
<style>
body {{ font-family: sans-serif; max-width: 700px; margin: auto; padding: 16px; }}
table {{ width: 100%; border-collapse: collapse; }}
td {{ padding: 6px; border-bottom: 1px solid #ddd; }}
</style>
</head>
<body>
<h1>🐇 AGROSAFE</h1>
<h2>Estado actual</h2>
<p style="font-size:1.3em">{estado_html}</p>
{foto_html}
<h2>Historial</h2>
<table>{filas}</table>
</body>
</html>"""


@app.route("/foto")
def foto():
    try:
        return send_file(FOTO_PATH, mimetype="image/jpeg")

    except Exception:
        return "Sin foto aún", 404


# Inicio del sistema
if __name__ == "__main__":
    try:
        hilo_sensores = threading.Thread(
            target=bucle_sensores,
            daemon=True
        )
        hilo_sensores.start()

        app.run(host="0.0.0.0", port=5000)

    except KeyboardInterrupt:
        print("Cierre solicitado por el usuario.")

    finally:
        GPIO.output(LED_PIN, GPIO.LOW)
        GPIO.cleanup()

        if camara is not None:
            camara.stop()
```
