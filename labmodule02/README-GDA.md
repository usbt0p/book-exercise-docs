# Gateway Device Application (Connected Devices)

## Lab Module 02

Be sure to implement all the PIOT-GDA-* issues.

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do? 

La implementación busca crear las funciones básicas de monitoreo del gateway para el sistema de IoT.
Para ello, se implementan las clases y métodos necesarios para monitorear el uso de CPU y memoria secundaria.
El sistema se lanza completamente a través de una aplicación, y permite loggear y monitorear todo el estado.
Toda la ejecución se automatiza a través de tareas programadas, que se ejecutan en un hilo separado en un intervalo fijo.

How does your implementation work?

Siguiendo un enfoque de arriba abajo, la implementación funciona de la siguiente forma:
- El componente más abstracto, y que sirve como punto de entrada del sistema, es la aplicación GatewayDeviceApp.
    Esta clase se encarga de inicializar el sistema y loggear cada paso, tanto exitos como errores.
    Por ahora, solo actúa como wrapper de SystemPerformanceManager.
- SystemPerformancemanager es núcleo de esta fase de la implementación. Se encarga de inicializar las tareas de monitoreo de CPU y memoria secundaria, y de loggear los resultados.
    Esto lo hace a través de dos clases hijas, SystemCpuUtilTask y SystemMemUtilTask, que implementan los métodos necesarios para obtener las mediciones.
    También se encarga de iniciar y detener las tareas de monitoreo, y de mantener un log de las mediciones.
    Nada más iniciarse, SystemPerformanceManager crea un future que permite ejecutar una tarea de forma asíncrona, y consultarla o cancelarla. Este future es un ScheduledExecutorService, que es una interfaz que permite ejecutar tareas en un intervalo fijo dentro de una pool de hilos (en este caso 1). La tarea pasada al ejecutor es una tarea Runnable que llama a handleTelemetry, que a su vez llama a las tareas de monitoreo de CPU y memoria secundaria.
- SystemMemUtilTask y SystemCpuUtilTask heredan ambas de BaseSystemUtilTask. Son clases que como mencioné anteriormente, encapsulan la función descrita en su nombre. Sus únicas funciones son encapsular una función que consigue la telemetría de la CPU o la memoria secundaria, y la devuelve. 

Notas del desarrollo:
- `mvn test -Dtest=GatewayDeviceAppTest` falla en PIOT-GDA-02-003. Se ejecuta el c´odigo como tal pero maven da un error largu´isimo en el stacktrace. Al desactivar los tests en el pom.xml, el código se ejecuta sin problemas. 
- Como hacer que el acceso a logger desde la clase BaseSystemUtilTask funcione en las demas clases hijas? Tiene que ser privado? Si meto un getter va a funcionar?

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/usbt0p/iot-java-components/tree/labmodule02


### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- SystemCpuUtilTaskTest
- SystemMemUtilTaskTest
- 

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- GatewayDeviceAppTest
- SystemPerformanceManagerTest
- 

EOF.
