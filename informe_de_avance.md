# **Sistema de Riego Inteligente**
## **Informe de Avances - WBS (Estructura de Desglose del Trabajo)**

### Integrantes del Grupo
| Padrón | Apellidos, Nombres | Fecha | Cuatrimestre |
| :----- | :--------------------- | :-----| :---|
| 112146 | Coluzzi, Santino Leonel | 20/11/2026 | 2do |
| 109894 | Kogan, Tobías Daniel | 20/11/2026 | 2do |
| 112119 | Rúa, Martino Manuel | 20/11/2026 | 2do |


A continuación se detalla el informe de avances del trabajo práctico final a partir de los requerimientos definidos en la propuesta del sistema.

| Estado | Descripción |
|:-----|:---------------------|
| 🟢 | Ya implementado |
| 🟡 | En proceso de implementarse |
| 🔴 | No se implementará / Pendiente |



| Nivel 1 (Proyecto) | Nivel 2 (Módulos) | Nivel 3 (Subsistemas) | Nivel 4 (Entregable) | Descripción del Requerimiento / Entregable | Estado |
| :---- |:-------|:-------|:--------| :------------- | :-------- |
| **1. Sistema de Riego Inteligente** | **1. Sensores** | **1.1 Variables Ambientales y Suelo** | 1.1.1.1 | Medición de temperatura ambiente mediante sensor analógico (ADC). | 🟡 |
| - | - | - | 1.1.1.2 | Medición de humedad del suelo mediante sensor analógico (ADC). | 🟡 |
| - | - | - | 1.1.3 | Medición de pH del suelo mediante sensor analógico (ADC). | 🟡 |
| - | - | - | 1.1.1.4 | Medición de iluminación ambiente mediante sensor analógico (ADC). | 🟡 |
| - | - | **1.2 Nivel de Tanques** |1.1.2.1 | Medición continua del nivel del tanque de agua mediante sensor analógico (ADC). | 🟡 |
| - | - | - | 1.1.2.2 | Medición continua del nivel del tanque de solución correctora mediante sensor analógico (ADC). | 🟡 |
| - | **2. Actuadores y Control** | **2.1 Control Hidráulico** | 1.2.1.1 | Válvula solenoide de riego accionada cuando la humedad cae por debajo del mínimo configurado. | 🟡 |
| - | - | - | 1.2.1.2 | Válvula solenoide de solución correctora accionada cuando el pH supera el umbral configurado. | 🟡 |
| - | - | - | 1.2.1.3 | Dosificación por volumen (sección del tanque × diferencia de altura + offset) con cierre automático al alcanzar la dosis. | 🟡 |
| - | - | **2.2 Control Climático y Lumínico** | 1.2.2.1 | Ventilador (12V) activado cuando la temperatura supera el umbral máximo configurado. | 🟡 |
| - | - | - | 1.2.2.2 | Lámpara blanca LED activada cuando la iluminación cae por debajo del umbral mínimo configurado. | 🟡 |
| - | **3. Modos y Seguridad** | **3.1 Selección de Modos** | 1.3.1.1 | DIP switch de encendido/apagado que lleva el sistema a modo APAGADO (actuadores y sensores en stand-by). | 🟡 |
| - | - | - | 1.3.1.2 | DIP switch MAN/AUTO para alternar entre modo MANUAL (nivel bajo) y AUTOMÁTICO (nivel alto). | 🟡 |
| - | - | - | 1.3.1.3 | Pulsador enclavado SET_UP para ingresar y salir del modo de configuración (apagando actuadores). | 🟡 |
| - | - | **3.2 Prioridades y Fallas** | 1.3.2.1 | Resolución jerárquica de modos en cada tick (1. APAGADO, 2. SET_UP, 3. FALLA, 4. MANUAL/AUTOMÁTICO). | 🟡 |
| - | - | - | 1.3.2.2 | Detección de tanque por debajo del nivel mínimo: finaliza entrega en curso, bloquea actuadores y entra en FALLA. | 🟡 |
| - | - | - | 1.3.2.3 | Salida automática del modo FALLA únicamente al detectar el rellenado por encima del nivel mínimo. | 🟡 |
| - | **4. Interfaz en Placa** | **4.1 Visualización y Alertas** | 1.4.1.1 | LCD 16x2 con expansor PCF8574 (bus I2C) para mostrar modo vigente, lecturas de sensores, menús y avisos. | 🟡 |
| - | - | - | 1.4.1.2 | Buzzer de alerta sonora activado ante nivel mínimo de tanque o límite de dosis de pH alcanzado. | 🟡 |
| - | - | **4.2 Navegación y Menús** | 1.4.2.1 | Botones NEXT, OK y BACK con antirrebote, activos exclusivamente en modos MANUAL y SET_UP. | 🟡 |
| - | - | - | 1.4.2.2 | Menú MANUAL para accionar actuadores (ON/OFF para ventilador/lámpara; selección de volumen para válvulas con validación de stock en tanque). | 🟡 |
| - | - | - | 1.4.2.3 | Menú SET_UP para editar umbrales, niveles mínimos y volúmenes de dosis (validando que la dosis no supere el nivel mínimo). | 🟡 |
| - | **5. Almacenamiento** | **5.1 Memoria No Volátil** | 1.5.1.1 | Almacenamiento de umbrales, niveles mínimos y volúmenes de dosis en Flash interna de la NUCLEO con verificación CRC. | 🟡 |
| - | - | - | 1.5.1.2 | Escritura en Flash ejecutada únicamente al salir de SET_UP si se confirmaron cambios (excepción documentada de WCET). | 🟡 |
| - | **6. Comunicación BLE** | **6.1 Telemetría Unidireccional** | 1.6.1.1 | Envío periódico por UART al módulo HM-10 (BLE) de tramas de texto con el modo, lecturas y avisos. | 🟡 |
| - | - | - | 1.6.1.2 | Visualización en tiempo real en aplicación móvil (operación autónoma del sistema si el teléfono está desconectado). | 🟡 |
| - | **7. Hardware y Tiempo Real** | **7.1 Electrónica y Potencia** | 1.7.1.1 | Diseño y fabricación de PCB a medida con soporte para NUCLEO-F103RB, etapas de potencia y periféricos. | 🟡 |
| - | - | - | 1.7.1.2 | Etapa de alimentación basada en fuente de 24V con reguladores a 12V, 5V y 3,3V. | 🟡 |
| - | - | **7.2 Arquitectura Firmware** | 1.7.2.1 | Ejecutor cíclico Bare Metal no bloqueante (`task_sensor`, `task_system`, `task_actuator`, `task_display`, `task_comm`) con vuelta menor a 1 ms. | 🟡 |




