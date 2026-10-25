# Software - AgroSafe

## 1. Descripción

Esta carpeta contiene el código fuente y la documentación del software del proyecto **AgroSafe**, un sistema de detección de movimiento diseñado para contribuir a la protección de cultivos frente a animales.

El sistema utiliza sensores para detectar movimiento y verificar la distancia del objeto detectado. Según las condiciones configuradas, activa una señal de respuesta representada mediante un LED durante las pruebas del prototipo.

## 2. Estructura de la carpeta

La carpeta se organizará de la siguiente manera:

- `src/`: código fuente principal del sistema.
- `docs/`: documentación técnica, instrucciones y diagramas del software.
- `requirements.txt`: dependencias de Python necesarias para ejecutar el programa, si corresponde.
- `README.md`: instrucciones de instalación, configuración y funcionamiento.

> Los archivos y subcarpetas deberán incorporarse según la estructura real del código disponible en el repositorio.

## 3. Tecnologías utilizadas

- **Plataforma:** Raspberry Pi 3 Model B+.
- **Lenguaje de programación:** Python.
- **Control de hardware:** GPIO Zero.
- **Sensores:** sensor infrarrojo PIR HC-SR501 y sensor ultrasónico HC-SR04.
- **Interfaz web:** Flask, si se encuentra implementada.
- **Actuador de prueba:** LED que representa la activación del sistema de respuesta.

## 4. Funcionamiento del sistema

El funcionamiento previsto del software contempla las siguientes etapas:

1. **Inicialización:** configuración de los pines y componentes conectados a la Raspberry Pi.
2. **Detección de movimiento:** lectura del sensor infrarrojo PIR.
3. **Verificación de distancia:** medición mediante el sensor ultrasónico HC-SR04.
4. **Evaluación de condiciones:** comprobación de si el objeto detectado se encuentra dentro del rango configurado.
5. **Activación de respuesta:** encendido del LED de prueba durante el tiempo establecido.
6. **Tiempo de espera:** pausa antes de permitir una nueva activación.

Los parámetros de referencia descritos en el avance del proyecto son una distancia inferior a 150 cm, una activación de 5 segundos y un tiempo de espera de 8 segundos. Estos valores deberán coincidir con los definidos en el código final.

## 5. Conexiones de referencia

| Componente | Pin GPIO | Pin físico |
|---|---:|---:|
| Sensor PIR HC-SR501 | GPIO 17 | 11 |
| LED de prueba | GPIO 18 | 12 |
| TRIG del HC-SR04 | GPIO 23 | 16 |
| ECHO del HC-SR04 | GPIO 24 | 18 |

**Importante:** estas son las conexiones de referencia del proyecto y deben verificarse con el montaje real. La salida ECHO del HC-SR04 puede trabajar a 5 V, por lo que se debe utilizar un divisor de tensión u otra adaptación apropiada para proteger la entrada de 3,3 V de la Raspberry Pi.

## 6. Instalación y configuración

### 6.1. Preparación

1. Utilizar una Raspberry Pi 3 Model B+ con un sistema operativo compatible.
2. Instalar Python 3.
3. Conectar los sensores y el LED de acuerdo con el esquema eléctrico del proyecto.
4. Descargar o clonar el repositorio de AgroSafe.

### 6.2. Instalación de dependencias

Las bibliotecas necesarias dependerán de las funciones implementadas en el código. Si el proyecto utiliza GPIO Zero, puede instalarse mediante:

```bash
sudo apt update
sudo apt install python3-gpiozero
```

Si se implementa una interfaz web con Flask, también deberá instalarse esa dependencia.

### 6.3. Ejecución

El nombre del archivo principal y el comando de ejecución deberán ajustarse al código definitivo. Por ejemplo, si el archivo principal se llama `main.py`, el comando sería:

```bash
python3 main.py
```

## 7. Parámetros de configuración

Los principales parámetros que deben documentarse en el código son:

- Distancia máxima de detección.
- Duración de la activación del actuador de prueba.
- Tiempo de espera entre activaciones.
- Pines GPIO utilizados por cada componente.

Los valores definitivos deberán corresponder a las constantes configuradas en el programa.

## 8. Pruebas del software

Las pruebas deben permitir verificar:

- Que el sensor PIR detecte movimiento.
- Que el sensor ultrasónico mida la distancia correctamente.
- Que la respuesta se active cuando se cumplan las condiciones establecidas.
- Que se respete el tiempo de activación y espera.
- Que el sistema se comporte correctamente cuando no detecte movimiento.

Los resultados deben registrarse después de ejecutar las pruebas físicas, indicando si cada una fue satisfactoria y adjuntando evidencias cuando estén disponibles.

## 9. Estado y limitaciones

El estado de implementación de cada función deberá actualizarse según las pruebas realizadas. No se debe considerar una función terminada únicamente porque esté documentada.

La activación de una bomba de agua u otro actuador real deberá documentarse y probarse por separado antes de afirmar que funciona correctamente.

## 10. Documentación complementaria

La documentación del software debe mantenerse coordinada con:

- El README principal del repositorio.
- La documentación de hardware.
- Los esquemas de conexión.
- Las evidencias de las pruebas realizadas.
- El informe y la presentación del proyecto.
