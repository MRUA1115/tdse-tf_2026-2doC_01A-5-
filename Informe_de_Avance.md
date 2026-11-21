<img src="https://www.fi.uba.ar/images/logo-fiuba.png" alt="FIUBA" width="50%">

# **Sistema de Riego Inteligente**

## **Informe de Avances - WBS (Estructura de Desglose del Trabajo)**

**Materia:** Taller de Sistemas Embebidos (TdSE)  
**Placa base:** STM32 NUCLEO-F103RB  
**Fecha:** 20/11/2026  
**Cuatrimestre:** 2do cuatrimestre 2026  

### Integrantes del Grupo
| Padrón | Apellidos, Nombres |
| :----- | :--------------------- |
| 112146 | Coluzzi, Santino Leonel |
| 109894 | Kogan, Tobías Daniel |
| 112119 | Rúa, Martino Manuel |

---

A continuación se detalla el informe de avances del trabajo práctico final a partir de los requerimientos definidos en `Propuesta.md`.

| Estado | Descripción |
| :---: | :--- |
| 🟢 | Ya implementado y verificado en la placa |
| 🟡 | En proceso de implementarse (o implementado sin verificar con el hardware definitivo) |
| 🔴 | No se implementará / Pendiente |

---

| Nivel 1 (Proyecto) | Nivel 2 (Módulos) | Nivel 3 (Subsistemas) | Nivel 4 (Entregable) | Descripción del Requerimiento / Entregable | Estado |
| :---- | :------- | :------- | :-------- | :------------- | :---: |
| **1. Sistema de Riego Inteligente** | **1. Sensores** | **1.1 Variables Ambientales y Suelo** | 1.1.1.1 | Medición de temperatura ambiente mediante sensor digital DHT22 (PA7, captura de entrada con TIM3). | 🟡 |
| - | - | - | 1.1.1.2 | Medición de humedad mediante sensor digital DHT22 (PA6, captura de entrada con TIM3). | 🟡 |
| - | - | - | 1.1.1.3 | Medición de pH mediante señal analógica por ADC (PA0), simulada con un potenciómetro lineal de 100 kΩ. | 🟢 |
| - | - | - | 1.1.1.4 | Medición de iluminación ambiente mediante LDR en divisor de tensión, leída por ADC (PA1). | 🟡 |
| - | - | **1.2 Nivel de Tanques** | 1.1.2.1 | Medición continua del nivel del tanque de agua mediante sensor de ultrasonido (TRIG PB4, ECHO PB10 con TIM2). | 🟡 |
| - | - | - | 1.1.2.2 | Medición continua del nivel del tanque de solución correctora mediante sensor de ultrasonido (TRIG PB5, ECHO PB11 con TIM2). | 🟡 |
| - | **2. Actuadores y Control** | **2.1 Control Hidráulico** | 1.2.1.1 | Válvula solenoide de riego accionada cuando la humedad cae por debajo del mínimo configurado. | 🟡 |
| - | - | - | 1.2.1.2 | Válvula solenoide de solución correctora accionada cuando el pH supera el umbral configurado. | 🟡 |
| - | - | - | 1.2.1.3 | Dosificación por volumen (sección del tanque × diferencia de altura + offset) con cierre automático al alcanzar la dosis. | 🟡 |
| - | - | **2.2 Control Climático y Lumínico** | 1.2.2.1 | Ventilador (12 V) activado cuando la temperatura supera el umbral máximo configurado. | 🟡 |
| - | - | - | 1.2.2.2 | Lámpara blanca LED activada cuando la iluminación cae por debajo del umbral mínimo configurado. | 🟡 |
| - | **3. Modos y Seguridad** | **3.1 Selección de Modos** | 1.3.1.1 | DIP switch de encendido/apagado que lleva el sistema a modo APAGADO (actuadores y sensores en stand-by). | 🟡 |
| - | - | - | 1.3.1.2 | DIP switch MAN/AUTO para alternar entre modo MANUAL (nivel bajo) y AUTOMÁTICO (nivel alto). | 🟡 |
| - | - | - | 1.3.1.3 | Pulsador enclavado SET_UP para ingresar y salir del modo de configuración (apagando actuadores). | 🟡 |
| - | - | **3.2 Prioridades y Fallas** | 1.3.2.1 | Resolución jerárquica de modos en cada tick (1. APAGADO, 2. SET_UP, 3. FALLA, 4. MANUAL/AUTOMÁTICO). | 🟡 |
| - | - | - | 1.3.2.2 | Detección de tanque por debajo del nivel mínimo: finaliza entrega en curso, bloquea actuadores y entra en FALLA. | 🟡 |
| - | - | - | 1.3.2.3 | Salida automática del modo FALLA únicamente al detectar el rellenado por encima del nivel mínimo (con histéresis). | 🟢 |
| - | **4. Interfaz en Placa** | **4.1 Visualización y Alertas** | 1.4.1.1 | LCD 16x2 con expansor PCF8574 (bus I2C) para mostrar modo vigente, lecturas de sensores, menús y avisos. | 🟡 |
| - | - | - | 1.4.1.2 | Buzzer de alerta sonora activado ante nivel mínimo de tanque o límite de dosis de pH alcanzado. | 🟡 |
| - | - | **4.2 Navegación y Menús** | 1.4.2.1 | Botones NEXT, OK y BACK con antirrebote, activos exclusivamente en modos MANUAL y SET_UP. | 🟡 |
| - | - | - | 1.4.2.2 | Menú MANUAL para accionar actuadores (ON/OFF para ventilador/lámpara; selección de volumen para válvulas con validación de stock en tanque). | 🟡 |
| - | - | - | 1.4.2.3 | Menú SET_UP para editar umbrales, niveles mínimos y volúmenes de dosis (validando que la dosis no supere el nivel mínimo). | 🟡 |
| - | **5. Almacenamiento** | **5.1 Memoria No Volátil** | 1.5.1.1 | Almacenamiento de umbrales, niveles mínimos y volúmenes de dosis en Flash interna de la NUCLEO con verificación CRC. | 🟡 |
| - | - | - | 1.5.1.2 | Escritura en Flash ejecutada únicamente al salir de SET_UP si se confirmaron cambios (excepción documentada de WCET). | 🟡 |
| - | **6. Comunicación BLE** | **6.1 Transmisión de Datos a la Aplicación** | 1.6.1.1 | Envío periódico por UART (USART1, PA9/PA10, 9600 baud) al módulo HM-10 (BLE) de tramas de texto con el modo, lecturas y avisos. | 🟡 |
| - | - | - | 1.6.1.2 | Visualización en tiempo real en aplicación móvil (operación autónoma del sistema si el teléfono está desconectado). | 🟡 |
| - | **7. Hardware y Tiempo Real** | **7.1 Electrónica y Etapa de Potencia** | 1.7.1.1 | Diseño y fabricación de PCB a medida con soporte para NUCLEO-F103RB, etapas de potencia y periféricos. | 🟡 |
| - | - | - | 1.7.1.2 | Etapa de alimentación basada en fuente de 24 V con reguladores a 12 V, 5 V y 3,3 V. | 🟡 |
| - | - | **7.2 Arquitectura Firmware** | 1.7.2.1 | Asignación de pines y configuración de periféricos en CubeMX (ADC1, TIM2, TIM3, USART1, I2C1 y GPIO de actuadores, botones y DIPs). | 🟢 |
| - | - | - | 1.7.2.2 | Ejecutor cíclico Bare Metal no bloqueante (`task_sensor`, `task_system`, `task_actuator`, `task_display`, `task_comm`) con vuelta menor a 1 ms. | 🟡 |

---

### Observaciones y Estado General del Desarrollo

* **Avances logrados:** *Ya está implementada la lectura de los seis sensores. El pH y la luz se leen por ADC, y el DHT22 y los ultrasonidos con captura de entrada de los timers. La lectura de pH se probó en la placa con un potenciómetro y funciona en todo el rango. Como todavía no tenemos todos los sensores, agregamos un modo de simulación: el potenciómetro se conecta al pin de cada sensor y así probamos humedad, temperatura y nivel de los tanques. También funciona el modo FALLA cuando un tanque queda bajo el mínimo y la salida automática cuando se rellena. Para la comunicación BLE ya están armadas las tramas que se envían al HM-10, y elegimos la app DSD TECH Bluetooth para el teléfono.*
* **Dificultades o demoras:** *Todavía no tenemos el módulo HM-10 ni los sensores de ultrasonido, así que esas partes no se pudieron probar con el hardware real. Los drivers del DHT22 y del ultrasonido solo se probaron con señales simuladas. Además, falta medir el tiempo de ejecución de cada tarea para confirmar que la vuelta del ejecutor cíclico sea menor a 1 ms.*
* **Ajustes de alcance:** *El sensor de pH se reemplaza por un potenciómetro, porque el sensor real es muy caro. Para temperatura y humedad usamos el DHT22, que es digital, y para el nivel de los tanques, sensores de ultrasonido, en lugar de los sensores analógicos de la Propuesta. Quedan pendientes los actuadores, la lectura de DIPs y botones, los menús del LCD y el guardado en Flash.*
