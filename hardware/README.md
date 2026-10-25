# Hardware - Documentación

## Contenido
El hardware de AgroSafe corresponde a un prototipo IoT diseñado para detectar la presencia de animales cerca de cultivos agrícolas y activar una respuesta disuasoria no letal.

El sistema utiliza una Raspberry Pi 3 B+ como unidad de procesamiento, junto con sensores de movimiento y distancia.

### 📁 Carpetas

#### `esquemas/`
Diagramas de circuitos y esquemáticos del sistema

#### `bom/`
Bill of Materials (Lista de materiales)

#### `fotos/`
Fotografías de alta resolución del prototipo ensamblado

---

## Instrucciones de Ensamble

### Componentes Principales
Componente: Raspberry Pi 3 B+. Función: Procesamiento de las señales y control del sistema.
Componente: Sensor PIR HC-SR501. Función: Detecta movimiento.
Componente: Sensor ultrasónico HC-SR04. Función: Mide la distancia a un objeto.
Componente: Protoboard. Función: Permite realizar las conexiones del circuito.
Componente: Cables jumper. Función: Conectan los componentes electrónicos.
Componente: LED indicador. Función: Representa la activación del rociador durante la demostración.
Componente: Mini bomba de agua. Función: Actuador previsto para el mecanismo de rociado.
Batería externa de 20.000 mAh. Función: Alimentación portátil del prototipo; especificaciones por verificar.

### Pasos de Ensamblaje
1. El sensor PIR detecta movimiento.
2. La Raspberry Pi procesa la señal.
3. El sensor ultrasónico mide la distancia.
4. Si el objeto está a menos de 150 cm, se activa el LED durante 5 segundos, según la lógica descrita para la demostración.
5. El sistema aplica un tiempo de enfriamiento de 8 segundos.
6. Los eventos pueden visualizarse en el dashboard web si este se encuentra ejecutándose.
 **Conexiones eléctricas**
Elemento: Salida del sensor PIR. GPIO de la Raspberrry Pi:GPIO 17, pin físico 11
Elemento: LED indicador. GPIO de la Raspberrry Pi:GPIO 18, pin físico 12
Elemento: TRIG del HC-SR04. GPIO de la Raspberrry Pi:GPIO 23, pin físico 16
Elemento: ECHO del HC-SR04. GPIO de la Raspberrry Pi:GPIO 24, pin físico 18, mediante divisor de voltaje

### Precauciones
-No conectar la señal ECHO del HC-SR04 directamente a un GPIO de la Raspberry Pi: debe adaptarse de 5 V a 3,3 V mediante un divisor de voltaje adecuado.
-Utilizar una resistencia de 220 Ω con el LED, según el montaje descrito.
-No alimentar la minibomba directamente desde un GPIO. Se requiere un circuito de accionamiento y una alimentación adecuados.
-Verificar la tensión, corriente y polaridad de todos los componentes antes de conectar la batería.
-Proteger la electrónica del contacto con agua y humedad.

## Especificaciones Técnicas

**Alimentación:**  
**Consumo:** 
**Dimensiones:** [mm x mm x mm]  
**Peso:** [gramos]

---

## Troubleshooting

| Problema | Posible Causa | Solución |
|----------|---------------|----------|
| [Problema 1] | [Causa] | [Solución] |
| [Problema 2] | [Causa] | [Solución] |
