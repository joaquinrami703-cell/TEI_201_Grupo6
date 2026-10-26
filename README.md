### Información del Equipo
- **Integrantes:**
  - Vanessa  Arévalo - Representante
  - Isidora Gonzalez- Miembro
  - Francisca Mardones - Miembro
  - Joaquin Ramírez - Miembro
  - Nicolas Torres - Miembro
  
- **ODS Seleccionado:** [ODS15: Vida de ecosistemas terrestres]
- **Problema a resolver:** [El conejo europeo es considerado una especie exótica invasora en Chile. Su presencia en grandes cantidades puede generar impactos tanto en terrenos agrícolas como en el entorno, debido principalmente al consumo de vegetación y a su rápida expansión.]

### Descripción del Proyecto
[Nuestro proyecto busca aportar a esta problemática mediante una alternativa de control no letal, orientada a detectar la presencia de conejos y alejarlos de las zonas cultivadas utilizando agua. De esta forma, se busca proteger las plantaciones de los agricultores del Choapa y, al mismo tiempo, evitar métodos que provoquen daño directo a los animales.]



### Arquitectura de Hardware
- **Cerebro del Sistema:** Raspberry Pi 3 B+
- **Detección de Movimiento:** Sensor PIR HC-SR501
- **Confirmación de Cercanía:** Sensor Ultrasónico HC-SR04
- **Actuador:** LED indicador (simulador de relé / bomba de agua)
- **Protección de Circuito:** Divisor de voltaje ($5\text{ V} \rightarrow 3.3\text{ V}$) en el pin Echo del sensor ultrasónico y resistencia de $220\,\Omega$ para el actuador.
- **Montaje:** Photoboard y cables jumper.
- **Alimentación:** Batería externa de 20.000 mAh

### Estado del Proyecto
- **Versión:** Avance 2 — Prototipo Alpha IoT. V3
- **Última actualización:** [19 de Octubre 2026]
- **Estado:** Prototipo V1

---

##  Estructura del Repositorio
```
├── hardware/          # Circuitos, esquemas, conexiones y lista de materiales.
├── software/          # Código Python, librerías y dashboard web.
├── diseno_3d/        # Modelos Fusion 360 y renders
├── testing/          # Plan de pruebas, resultados y evidencias.
├── documentacion/    # Informes, presentaciones y manuales.
└── iteraciones/      # Historial de cambios y mejoras del prototipo.
```

---

##  Inicio Rápido

### Requisitos Previos
-Raspberry Pi 3 B+.
-Python 3.
-GPIO Zero.
-Flask.
-Sensores PIR HC-SR501 y ultrasónico HC-SR04.

### Instalación
1. Clonar el repositorio.
2. Revisar las dependencias documentadas en software/.
3. Conectar los sensores según el esquema de hardware/.
4. Ejecutar el programa principal de Python en la Raspberry Pi.
5. Si el dashboard está implementado, acceder desde un dispositivo conectado a la misma red Wi-Fi utilizando la dirección y el puerto configurados.

---

##  Checklist de Entrega

### Hardware ✓
- [ ] Esquema eléctrico de Raspberry Pi, sensores y actuadores.
- [ ] Lista de materiales (BOM) con cantidades y especificaciones.
- [ ] Fotografías del prototipo ensamblado.
- [ ] Documentación de alimentación y conexiones GPIO.

### Software ✓
- [ ] Código Python comentado y subido a softwar/.
- [ ] Librerías y dependencias documentadas.
- [ ] Instrucciones de instalación y ejecución.
- [ ] Dashboard Flask documentado, si está implementado.
- [ ] Código probado en la Raspberry Pi.

### Diseño 3D ✓
- [ ] Archivos originales de Fusion 360 (.f3d), si se utilizó.
- [ ] Renders del diseño desde distintos ángulos.
- [ ] Planos técnicos y dimensiones.
- [ ] Estado de fabricación y montaje documentado.

### Testing ✓
- [ ] Plan de pruebas.
- [ ] Evidencias fotográficas/videos
- [ ] Resultados reales de las pruebas de sensores y actuadores.
- [ ] Registro de errores y mejoras.
- [ ] Pruebas con usuarios, según los requisitos del curso.

### Documentación ✓
- [ ] README principal actualizado.
- [ ] README de hardware y software actualizados.
- [ ] Informe final y presentación.
- [ ] Referencias técnicas y fichas de los componentes.
- [ ] Limitaciones y trabajos pendientes documentados.




---

##  Licencia
Este proyecto es desarrollado como parte del curso TEI201 - Facultad de Ingenieria y Ciencias - Universidad Adolfo Ibañez
