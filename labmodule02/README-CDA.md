# Constrained Device Application (Connected Devices)

## Lab Module 02

Be sure to implement all the PIOT-CDA-* issues (requirements).

### Description

NOTE: Include two full paragraphs describing your implementation approach by answering the questions listed below.

What does your implementation do?

La implementación es la base del sistema, permitiendo la recogida de telemetría de memoria y CPU para su gestión.

How does your implementation work?

Una clase base se crea para las tareas de adquisición de telemetría, que son dos; 
medición de memoria y de uso de la CPU. Cada una de estas tareas tiene a su vez una clase propia e implementa un método 
para obtener las mediciones. Estas clases se llaman desde la app principal a 
través del método `handleTelemetry` del gestor de performance, y así se mantiene el monitoreo del sistema.
Este gestor también se encarga de iniciar y detener las tareas de adquisición de telemetría, 
de mantener un log de las mediciones y de inicializar ciertas configuraciones del sistema como `pollRate`
y `locationID`.

Incluí esto para acordarme de lo que hacía a medida que iba completando las tareas:
- PIOT-CDA-02-000: todos los tests de `labmodule01` pasan.
- PIOT-CDA-02-001: mantuve el esqueleto sugerido para `ConstrainedDeviceApp`. Todos los tests pasan.
- PIOT-CDA-02-002: implementé los métodos `__init__` y demás en `SystemPerformanceManager` tal y como se sugería en esta tarea. Todos los tests pasan.
- PIOT-CDA-02-003: creé una instancia de `SystemPerformanceManager` asociada al `ConstrainedDeviceApp` y la inicialicé en los métodos de start y stop y en el `__init__` de `ConstrainedDeviceApp` y en los . Todos los tests pasan, en el output se observa que los logs de ambos sistemas se intercalan en la consola.
- PIOT-CDA-02-004: implementé los métodos como se sugiere, añadiendo decoradores a las propiedades, y hice que la clase `BaseSystemUtilTask` implemente `getTelemetryValue` como un método abstracto para futura implementación.
- PIOT-CDA-02-005: implementé `testGetTelemetryValue()` y `__init__`, pasado el test `testGetTelemetryValue`.
- PIOT-CDA-02-006: implementé `testGetTelemetryValue()` y `__init__`, pasado el test `testGetTelemetryValue`.
- PIOT-CDA-02-007: modifiqué __init__, implementé handleTelemetry, startManager y stopManager en SyetemPerformanceManager. El test pasa.
- PIOT-CDA-02-100: todos los tests de labmodule02 pasan. Merge con default.

### Code Repository and Branch

NOTE: Be sure to include the branch.

URL: https://github.com/usbt0p/iot-python-components/tree/labmodule02

### Unit Tests Executed

NOTE: The instructor will execute your unit tests. You only need to list each test case below
(e.g. ConfigUtilTest, DataUtilTest, etc). Be sure to include all previous tests, too,
since you need to ensure you haven't introduced regressions.

- SystemCpuUtilTaskTest
- SystemMemUtilTaskTest
- ConfigUtilTest

### Integration Tests Executed

NOTE: The instructor will execute most of your integration tests using their own environment, with
some exceptions (such as your cloud connectivity tests). In such cases, they'll review
your code to ensure it's correct. As for the tests you execute, you only need to list each
test case below (e.g. SensorSimAdapterManagerTest, DeviceDataManagerTest, etc.)

- ConstrainedDeviceAppTest
- SystemPerformanceManagerTest
- 

EOF.
