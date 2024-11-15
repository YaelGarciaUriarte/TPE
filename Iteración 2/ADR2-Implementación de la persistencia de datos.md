# ADR2: Implementación de la persistencia de datos
 
## Contexto y planteamiento del problema

En el sistema actual, la persistencia de datos se gestiona mediante dos bases de datos relacionales SQL centralizadas: una para los datos de clientes y pagos, y otra para los pedidos. Estas bases de datos actúan como un único punto de acceso para toda la lógica de negocio, generando fuertes dependencias entre los módulos funcionales que implica que cualquier cambio o fallo en las bases puede impactar significativamente en todo el sistema. 


## Factores que impulsan la toma de decisiones

- Modificabilidad: la nueva arquitectura debe ser menos rígida y más fácil de evolucionar y actualizar.

- Escalabilidad: El sistema debe atender un número cada vez mayor de pedidos por hora.

- Desplegabilidad: cada servicio debe poder desplegarse de forma independiente.


## Resultado de la decisión

La decisión tomada es implementar un modelo de persistencia descentralizado donde cada microservicio tendrá su propia base de datos independiente, adaptada a sus necesidades específicas. Esto garantiza independencia y escalabilidad, permitiendo a cada microservicio evolucionar de manera autónoma sin generar dependencias entre ellos.
Para garantizar consistencia y sincronización entre las bases de datos de los microservicios que interactúan frecuentemente, se adoptarán estrategias como Event Sourcing, que registra cada cambio como un evento para reconstruir el estado actual de manera confiable, o Saga, que coordina transacciones distribuidas entre microservicios asegurando consistencia eventual, lo cual se terminará de decidir en etapas posteriores.


## Otras opciones consideradas

- Base de Datos Compartida: implica que todos los microservicios accedan y compartan una base de datos centralizada, lo que genera dependencia de una infraestructura de almacenamiento común. Esta opción no se elige porque, aunque simplifica la gestión de los datos y garantiza la consistencia inmediata entre servicios, introduce un acoplamiento fuerte entre los microservicios, dificultando la autonomía de cada uno y limitando la escalabilidad del sistema.

- Service Data Replication (Replicación de Datos de Servicio): consiste en replicar los datos entre microservicios para que cada uno tenga copias locales de los datos necesarios, sin necesidad de consultar continuamente otros microservicios o a la base de datos maestra. Esta estrategia mejora la disponibilidad y la velocidad de acceso a los datos, pero no se seleccionó debido a la complejidad adicional que puede generar en la gestión de datos, así como al riesgo de inconsistencias temporales entre las réplicas si no se maneja adecuadamente.


## Consecuencias

### Ventajas:

- Independencia y Encapsulamiento: cada microservicio tiene control sobre sus datos y esquemas lo que facilita la evolución independiente de los servicios sin riesgo de afectar a otros.

- Aislamiento de fallos: un problema en la base de datos de un microservicio no afecta a otros servicios.

- Escalabilidad Independiente: es posible escalar servicios y sus bases de datos de manera independiente, optimizando el uso de recursos según las demandas específicas.

- Diversidad de tecnología: las bases de datos pueden tener diferentes tecnologías (SQL, NoSQL, etc.) según las necesidades específicas de cada servicio.

### Desventajas:

- Consistencia de datos: se requieren implementar mecanismos adicionales para los datos compartidos entre microservicios para mantener la coherencia.

- Costos: de la incorporación de las bases de datos y el mecanismo para mantener la consistencia entre las bases de datos.
