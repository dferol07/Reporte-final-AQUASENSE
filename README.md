# Reporte-final-AQUASENSE
## Breve descripción del proyecto
Aquasense es un sistema de Internet de las Cosas (IoT) diseñado para monitorear en tiempo real la calidad del agua en los pozos de agua potable en Tlaxcoapan Hidalgo.  Su propósito principal es el monitoreo constante en los pozos para estar al tanto de la calidad de agua que llagan a las casas de la comunidad.
El alcance del proyecto incluye la medición de parámetros clave en los pozos de Tlaxcoapan  la transmisión de estos datos hacia una estación receptora central, y su posterior envío a un servidor donde son almacenados, procesados ​​y visualizados para su análisis por técnicos, autoridades de Casth.

## Tecnologías utilizadas
#### Sensores :
Sensor de Conductividad ductividad
Sensor de turbidez
Sensor de pH

#### Microcontrolador :
LILYGO T-SIM7000G ESP32 con conectividad GPRS
LoRa
#### Tecnologías de comunicación :
LoRa para comunicación de largo alcance entre nodos sensores y la estación receptora
ESP-NOW (WiFi) para comunicación punto a punto entre dispositivos locales
GPRS para el envío de datos hacia el servidor IoT a través de redes móviles

#### Servidor IoT (Raspberry Pi con IoTStack):
Mosquitto (corredor MQTT)
Node-RED (procesamiento de datos)
InfluxDB (base de datos de series temporales)
Grafana (visualización de datos en paneles de control)

#### Visualización :
Dashboards dinámicos de datos históricos en Grafana y en tiempo real en Node-RED accesibles por navegador web
Diagrama de topología lógica del sistema.
La topología lógica del proyecto Aquasense está compuesta por varias secciones interconectadas que permiten el flujo continuo de datos desde el campo hasta la visualización en tiempo real por parte del usuario. A continuación se describe el recorrido de la información y cómo interactúan los componentes:

#### Nodos sensores remotos
Son estaciones instaladas dentro de los pozos de Tlaxcoapan.. Cada nodo cuenta con sensores para medir parámetros del agua como pH, turbidez y conductividad. Estos sensores están conectados a una placa LoRa 32 v3 encargada de recolectar los datos y transmitirlos inalámbricamente.

#### Estación receptora
Se encuentra dentro del área de cobertura LoRa de los nodos remotos. Esta estación recibe los datos mediante LoRa y los transfiere a otro microcontrolador LILYGO T-SIM7000G con módulo GPRS , utilizando comunicación ESP-NOW . La separación entre recepción y transmisión permite modular la arquitectura.

#### Red celular (GPRS)
Una vez que los datos llegan a la estación con GPRS, se envían a través de la red móvil al servidor central. Esta comunicación permite transmitir información desde zonas rurales sin necesidad de infraestructura de red fija.

#### Servidor IoT
Ubicado en una Raspberry Pi , este servidor ejecuta una pila de herramientas IoT:

Mosquitto (MQTT) para recibir los datos de forma eficiente.
Node-RED para procesar, filtrar y redirigir la información.
InfluxDB para almacenar los datos en series temporales.
Grafana para construir paneles de visualización.
Usuario final
Tecnicos, vigilantes de pozos y los encargados de Casth pueden acceder a los paneles de control desde navegadores web, ya sea en computadoras o teléfonos inteligentes, para visualizar los niveles de calidad del agua en tiempo real y tomar decisiones informadas.

#### Flujo general de información:
Sensores → LoRa con sensores → Comunicaión LoRa → LoRa receptora → Transmisión por ESP-NOW → LILYGO T-SIM7000G con GPRS → Red celular → Servidor IoT (MQTT → Node-RED → InfluxDB → Grafana) → Usuario final.

Este diseño modular y escalable permite implementar múltiples nodos sensores en distintas ubicaciones, mantener la eficiencia energética en campo y garantizar una interfaz de consulta centralizada para los usuarios.
