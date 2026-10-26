#  Archivos Fusion 360 (Diseño 3D y Encapsulado)

Actualmente, los modelos 3D del encapsulado y componentes se presentan como **piezas independientes** para la evaluación del Avance #2. 

> **Nota de Iteración y Mejora Continua (Avance #3):**  
> En la evaluación presencial del Avance #2 se identificó la necesidad de integrar un **ensamble completo con restricciones físicas (*Joints*) y árbol de componentes unificado**. Siguiendo la retroalimentación del docente, la versión actual contiene las piezas por separado, mientras que para el **Avance #3** se entregará el archivo `.f3d` unificado con el ensamble final, historial de timeline y restricciones de movimiento (torreta giratoria).

---

##  Archivos Disponibles (Avance #2)

En la carpeta [`/diseno_3d`](./diseno_3d/) se encuentran los modelos individuales del diseño conceptual:

1. **`base_fija.f3d` / `.stl`:** Base principal de $13.2 \times 13.2 \times 20.3\text{ cm}$. Aloja la Raspberry Pi 3 B+, la protoboard y el circuito de alimentación.
2. **`torreta_giratoria.f3d` / `.stl`:** Torreta superior de $5.9 \times 8.1 \times 8.8\text{ cm}$. Alberga los sensores (PIR y Ultrasónico) y el brazo/boquilla con espacio para servomotor.

---

##  Estructura Proyectada para Ensamble Final (Avance #3)

### Árbol de Componentes
```text
Agrosafe_Ensamble_Completo
├── Base_Inferior_Chasis
├── Tapa_Removible_Mantenimiento
├── Torreta_Giratoria_Sensores
├── Raspberry_Pi_3B_DevBoard
├── Sensor_PIR_HC-SR501
├── Sensor_Ultrasonico_HC-SR04
└── Tornilleria_y_Soportes
