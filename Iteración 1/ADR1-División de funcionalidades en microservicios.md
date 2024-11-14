# ADR1: División de funcionalidades en microservicios

## Contexto y planteamiento del problema

Actualmente, la compañía de productos alimenticios utiliza una arquitectura monolítica que dificulta la escalabilidad y la evolución del sistema. Además, todos los servicios del sistema  están empaquetados en un único artefacto para despliegue que implica que cualquier cambio en la aplicación, requiera un re-despliegue de toda la aplicación.


## Factores que impulsan la toma de decisiones

- Modificabilidad: la nueva arquitectura debe ser menos rígida y más fácil de evolucionar y actualizar.
  
- Escalabilidad: El sistema debe atender un número cada vez mayor de pedidos por hora.
  
- Desplegabilidad: cada servicio debe poder desplegarse de forma independiente.


## Resultado de la decisión

La migración a microservicios es la opción que satisface completamente los requisitos fundamentales de modificabilidad, escalabilidad y capacidad de despliegue. Esta arquitectura permite optimizar la infraestructura para que el sistema pueda evolucionar y adaptarse con flexibilidad a nuevas necesidades.
Los microservicios resultantes de la división son: Clientes, Pedidos, Repartos y rutas, Pagos, Estadísticas e Incidencias.
Cada microservicio expondrá sus funcionalidades mediante un API Rest y se utilizará una API Gateway para centralizar el acceso a los servicios y gestionar peticiones de clientes. 


## Otras opciones consideradas

- Mantener la arquitectura monolítica con mejoras internas: aunque se podrían realizar algunos cambios en la arquitectura monolítica para mejorar ciertos aspectos de rendimiento y organización, seguiría existiendo la dependencia de un único despliegue.
  
- Arquitectura basada en servicios (SOA): similar a los microservicios, pero con servicios menos independientes, a menudo gestionados centralmente mediante un bus de servicios empresariales (ESB) pero esto puede limitar la escalabilidad y agregar complejidad operativa, además de no permitir una completa autonomía de cada servicio.


## Consecuencias

### Ventajas:

- Mejora de la Modificabilidad: Al separar cada funcionalidad en microservicios independientes, cada uno puede evolucionar y modificarse de forma aislada, sin impactar al resto del sistema.
  
- Aumento de la Escalabilidad: Los microservicios permiten escalar únicamente los módulos que requieren mayor capacidad, optimizando los recursos y adaptándose mejor a la demanda.

- Facilidad de Despliegue: Los microservicios pueden desplegarse de forma individual, lo que permite actualizaciones y correcciones en un módulo sin afectar a los demás.

### Desventajas:

- Complejidad en la gestión: administrar múltiples servicios independientes implica una mayor complejidad operativa en términos de monitoreo, logging, y gestión de la comunicación entre servicios.

- Costos iniciales de migración: la reestructuración del sistema y el cambio a una arquitectura de microservicios conlleva un costo de tiempo y recursos en la etapa de migración. 

- Necesidad de conocimientos en microservicios: para la migración se requiere un equipo de desarrolladores con experiencia en microservicios, lo cual puede implicar la necesidad de capacitación adicional o la contratación de especialistas.

