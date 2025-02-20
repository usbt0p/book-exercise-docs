# Constrained Device Application (Connected Devices)

## Lab Module 03

Be sure to implement all the PIOT-CDA-* issues (requirements).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

Esta implementación se encarga de implementar la simulación de sensores y actuadores en el
ConstrainedDeviceApp, y de definir templates de tipos de datos para cada uno. 
Se implementan datos base de un dispositivo IoT, y de ahí se derivan los datos de sensores y actuadores. Estos contienen info como nombre, id, valor,  
También se implementan los sensores de humedad, presión y temperatura, y los actuadores
de humificador y HVAC (heating, ventilation, and air conditioning). Los sensores generan telemetría (datos como temperatura, huedad, etc...) y los actuadores simulan activación/desactivación en función de su estado.
Además, se incluyen clases que las aúnan y gestionan, como SensorAdapterManager, ActuatorAdapterManager y DeviceDataManager. 


How does your implementation work?

Describiré el funcionamiento de la implementación de abajo arriba.

1. Primero se implementa la clase BaseIotData, que sirve como base para ActuatorData, SensorData y SystemPerformanceData. En ella
se incluyen los atributos básicos de los tipos de datos (type, ide, status, name, value...) a parte de 
sus respectivos getters y setters. Las dos clases hijas simplemente añaden datos específicos de actuadores 
y sensores, sus getters y setters, y métodos mágicos __str__.

2. Luego, se implementan los sensores, empezando por la clase base BaseSensorSimTask, que implementa información base de sensores
y métodos de generación de telemetría, es decir, la información / metadatos de un sensor genérico. 
De ella heredan los sensores de temperatura, presión y humedad. Estos simplemente heredan los atributos de
la clase superior, aunque en un futuro generarán información propia simulada a través del parámetro dataSet del constructor.

3. A continuacíon la implementación se hace de forma similar a la anterior en BaseActuatorSimTask. Los actuadores
también guardan un tipo de BaseIotData, en este caso ActuatorData. En esta se contienen sus estados y últimas respuestas.
Los actuadores se activan o desactivan (de forma simulada a través de data y logs) cuando se les pasa un comando.
Las clases que heredan de esta, HVAC y Humidifier, simplemente implementan el constructor del padre.

4. A continuación se implementa la clase SensorAdapterManager. Esta tiene como objetivo  gestionar todos
los sensores del sistema desde un solo punto. Su constructor determina las configuraciones de los sensores, 
como la frecuencia de actualizaciones, emulación de los datos y sensores utilizados (hay más, pero no se trata de lsitarlos todos).
Tiene también sus respectivos métodos de inicialización y parada de los sensores, así como un método 
de gestión de la telemetría de todos ellos.

5. ActuatorAdapterManager sigue los mismos principios que el gestor anteriormente mencionado. La única diferencia 
destacable es en lugar de gestionar telemetría, gestiona los comandos enviados a los actuadores, y los 
updates de cada uno, que son los que llevan a realizar activaciones y desactivaciones.

6. Casi el último. Siguiendo la tónica general, DeviceDataManager reúne la funcionalidad de los 2 gestores
anteriormente descritos + la performance del sistema con SystemPerformanceManager.
O sea, contiene metodos para iniciar y parar SystemPerformanceManager y SensorAdapterManager, y métodos para 
recibir mensajes y enviar respuestas para el ActuatorAdapterManager.
A parte de esto, claro, el constructor configura todo lo necesario a la hora de la inicialización.

7. Finalmente, se cierra el círculo. Una instancia de DeviceDataManager se crea en ConstrainedDeviceApp, 
el punto de entrada inicial de la aplicación. Recordemos que este llama a los gestores, que llaman a sensores
, actuadores y sistemas de monitoreo, que a su vez utilizan otras clases de utilidad específicas y plantillas 
de tipos de datos como las que vimos en el punto 1 de esta descripción. Para esta implementación, como
en la mayoría de las anteriores, me ceñí al código de ejemplo e intenté comprenderlo más que modificarlo. 
Por ello tal y como se sugiere, esta clase implementa métodos start y stop que llaman al DeviceDataManager, 
y se eliminan las referencias a SystemPerformanceManager ya que ya están contenidas en el otro gestor.
Finalmente, un bucle potencialmente infinito ejecuta todo deste el main.

8. Finalmente, merge de la branch ya que todos los tests unitarios y de integración pasan correctamente.


### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/usbt0p/iot-python-components/tree/labmodule03

### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- ActuatorDataTest
- SensorDataTest
- SystemPerformanceDataTest
- HumiditySensorSimTaskTest
- PressureSensorSimTaskTest
- TemperatureSensorSimTaskTest
- HumidifierActuatorSimTaskTest
- HvacActuatorSimTaskTest
- Literally every other possible test there was

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- SensorAdapterManagerTest
- ActuatorAdapterManagerTest
- DeviceDataManagerNoCommsTest
- ConstrainedDeviceAppTest
- SystemPerformanceManagerTest
- Literally every other possible test there was

EOF.
