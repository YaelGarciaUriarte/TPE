# ADR3: estrategia de consistencia de datos
 
## Contexto y planteamiento del problema

En este sistema basado en microservicios, cada servicio gestiona su propia base de datos para garantizar la autonomía y la escalabilidad. Sin embargo, surge el desafío de mantener la consistencia de los datos entre los microservicios que interactúan frecuentemente o dependen unos de otros para llevar a cabo los procesos. Para esto, es crucial definir una estrategia adecuada que permita manejar esta consistencia sin comprometer la disponibilidad, la escalabilidad o el rendimiento del sistema.


## Factores que impulsan la toma de decisiones


- Escalabilidad: El sistema debe atender un número cada vez mayor de pedidos por hora.

- Además, la decisión en la iteración anterior donde implementamos un modelo de persistencia de datos nos indica la necesidad de mantener la consistencia y sincronización entre microservicios que interactúan frecuentemente.


## Resultado de la decisión

Se ha decidido implementar una estrategia basada en Event Sourcing. A través de este enfoque, cada microservicio mantendrá su propia base de datos local, pero sincronizará su estado con otros servicios a través de eventos, lo que asegura que, eventualmente, todos los microservicios estarán alineados con los mismos datos. 

Para garantizar la consistencia eventual, los microservicios escucharán los eventos de otros servicios a través de un mecanismo de mensajería asíncrona, como una cola de eventos. Este enfoque reduce la dependencia directa entre servicios y evita las transacciones distribuidas, lo que mejora la escalabilidad y la disponibilidad del sistema.
Además, esta estrategia permitirá almacenar todos los eventos que representan los cambios de estado de las entidades en un Event Store.


## Otras opciones consideradas

- Patrón Saga: es una estrategia donde en lugar de utilizar transacciones distribuidas, se divide una transacción larga en una serie de pasos locales, cada uno realizado por un microservicio. Si un paso falla, se requiere que se ejecuten acciones de compensación para revertir los cambios realizados hasta ese momento (cada servicio implementa estas acciones), lo que puede ser complejo y propenso a errores si no se gestionan adecuadamente los flujos de control y los fallos.

- Interacción Directa entre Microservicios: cada microservicio mantiene su propia base de datos y la consistencia de los mismos se asegura mediante la comunicación directa y el intercambio de mensajes. Este enfoque permite una arquitectura más simple pero puede resultar en dependencias más fuertes entre los microservicios, lo que dificulta la escalabilidad y la resiliencia del sistema a medida que crece. 


## Consecuencias

### Ventajas:

- Consistencia entre microservicios: Permite que todos los servicios relacionados mantengan y reconstruyan el estado de los datos de manera consistente y sincronizada.

- Desacoplamiento: Los microservicios pueden suscribirse a los eventos y reaccionar de forma independiente, lo que facilita la integración entre microservicios sin acoplamiento directo.

- Historial completo: Permite mantener un registro detallado de todos los cambios que han ocurrido en el sistema.

- Escalabilidad: Permite que los microservicios manejen eventos de manera independiente, reduciendo la necesidad de comunicación directa entre ellos y mejorando la escalabilidad del sistema.

### Desventajas:

- Complejidad adicional: Introduce complejidad en el diseño y la implementación.

- Necesidad de almacenamiento extra: se necesitan bases de datos adicionales para almacenar los eventos.
