# Aplicación del Método ADD
Este documento describe el trabajo realizado en cada iteración del Método ADD para el diseño arquitectónico del sistema.

## Paso 1: Revisión de Entradas
### Entradas analizadas:
#### - Propósito del diseño: 
Migrar de una arquitectura monolítica a una arquitectura basada en microservicios que es más flexible y escalable.

#### - Requerimientos funcionales principales: 
Gestión de clientes, pedidos, pagos, rutas, estadísticas e incidencias.

[Requerimientos Funcionales](https://github.com/YaelGarciaUriarte/TPE/blob/main/Requerimientos/RequerimientosFuncionales.md)

#### - Escenarios de atributos de calidad:

- **Modificabilidad:** "Cuando un desarrollador solicite un cambio en la lógica de negocio, el sistema deberá permitir la implementación, prueba y despliegue del cambio en menos de 2 días, sin que esto afecte otros servicios o funcionalidades del sistema." 

- **Escalabilidad:** “A medida que el número de usuarios crezca el sistema deberá escalar automáticamente para manejar el incremento sin impactar la experiencia del usuario, manteniendo un tiempo de respuesta promedio por debajo de 1 segundo.”

- **Performance:** ”Cuando un usuario consulte el estado de su pedido, el sistema deberá completar la solicitud y devolver los detalles del pedido en menos de 300 milisegundos durante una operación normal.“

- **Desplegabilidad:** “Cuando se requiera desplegar un nuevo microservicio, el sistema deberá permitir el despliegue del servicio de forma independiente en menos de 15 minutos, sin interrumpir la operación de otros servicios en ejecución.” 

- **Seguridad:** “El sistema deberá autenticar a los usuarios y asignar roles adecuados para que solo los usuarios con permisos correctos accedan a funciones específicas. Cualquier intento de acceso no autorizado será denegado y registrado.”

  *Las medidas de respuesta son suposiciones.*

[Atributos de Calidad](https://github.com/YaelGarciaUriarte/TPE/blob/main/Requerimientos/AtributosDeCalidad.md)

#### - Restricciones: 
Limitaciones técnicas del equipo, tiempo y recursos para la implementación inicial. (Suposiciones)

#### - Preocupaciones arquitectónicas: 
Escalabilidad, independencia de módulos y facilidad de despliegue.  



# Aplicación del Método ADD en la Iteración 1: División de funcionalidades en microservicios

## Paso 2: Establecer el objetivo de la iteración seleccionando los drivers

- **Drivers seleccionados:**

  * Modificabilidad.

  * Escalabilidad.

  * Desplegabilidad.
- **Objetivo de la iteración:** Diseñar una solución que permita separar responsabilidades funcionales en microservicios independientes.

## Paso 3: Seleccionar uno o más elementos del sistema a refinar
- **Elemento seleccionado:** La estructura monolítica actual.
- **Decisión:** Dividir las responsabilidades funcionales en módulos autónomos que luego se implementarán como microservicios.

## Paso 4: Elegir conceptos de diseño para satisfacer los drivers seleccionados

- **Alternativas evaluadas:**
  * Mantener la arquitectura monolítica con mejoras internas.
  * Migrar a una arquitectura basada en servicios (SOA).
  * Adoptar una arquitectura de microservicios.
- **Alternativa seleccionada:** Arquitectura de microservicios.
- **Justificación:**
  * Cumple mejor con los drivers seleccionados en la iteración.
  * Aumenta la independencia de módulos y permite una mayor flexibilidad en el desarrollo.

## Paso 5: Instanciar elementos arquitectónicos, asignar responsabilidades y definir interfaces
- Se definieron los siguientes microservicios:
  * **Clientes:** Maneja toda la información personal de los clientes y su autenticación.
  * **Pedidos:** Gestiona la creación, procesamiento y seguimiento de pedidos.
  * **Repartos y rutas:** Gestiona la asignación de rutas para los camiones de reparto, la asignación de flotas y optimiza las rutas.
  * **Pagos:** Gestiona la interacción con el sistema de pagos de MercadoLibre para procesar pagos de los clientes.
  * **Estadísticas:** Recopila y proporciona estadísticas.
  * **Incidencias:** Gestiona el registro y seguimiento de incidencias en el reparto.
- Cada microservicio expondrá su funcionalidad mediante una API REST, con una API Gateway para centralizar las peticiones de los clientes.

## Paso 6: Esbozar vistas y registrar decisiones
- **Registro de decisiones:**
  * En el ADR1 se registran las decisiones clave que incluyen la separación de responsabilidades en microservicios, el uso de APIs independientes para cada servicio y el agregado de un API Gateway para gestionar las peticiones de los clientes.

    [ADR1: División de funcionalidades en microservicios](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%201/ADR1-Divisi%C3%B3n%20de%20funcionalidades%20en%20microservicios.md)

- **Vista creada:**
  * Un diagrama de componentes que muestra los microservicios principales y su interacción entre ellos y con los clientes a través de la API Gateway.

    [Vista microservicios](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%201/vista-microservicios.md)

## Paso 7: Realizar un análisis del diseño actual
- **Evaluación de la solución:**
  * Se confirmó que la arquitectura propuesta satisface los atributos de calidad priorizados (modificabilidad, escalabilidad y desplegabilidad).
- **Tradeoffs aceptados:**
  * **Tradeoff entre simplicidad y escalabilidad:** La arquitectura de  microservicios satisface los requerimientos de escalabilidad a largo plazo pero agrega mayor complejidad operativa.
  * **Tradeoff entre independencia y costos iniciales:** Los microservicios ofrecen mayor independencia, pero generan costos de tiempo y recursos en la etapa de migración.
  * **Tradeoff entre autonomía y complejidad:** La adopción de microservicios introduce desafíos en la gestión de múltiples servicios y la comunicación entre ellos para mantener la autonomía de los mismos.


# Aplicación del Método ADD en la Iteración 2: Implementación de la persistencia de datos

## Paso 2: Establecer el objetivo de la iteración seleccionando los drivers
- **Drivers seleccionados:**
  * Modificabilidad. 
  * Escalabilidad.
  * Desplegabilidad. 
- **Objetivo de la iteración:** Diseñar un modelo de persistencia de datos independiente para cada microservicio.

## Paso 3: Seleccionar uno o más elementos del sistema a refinar
- **Elemento seleccionado:** El subsistema de persistencia centralizado actual.
- **Decisión:** Migrar a un modelo donde cada microservicio gestione su propia base de datos.

## Paso 4: Elegir conceptos de diseño para satisfacer los drivers seleccionados
- **Alternativas evaluadas:**
  * Base de datos compartida.
  * Service Data Replication.
  * Bases de datos independientes por microservicio.
- **Alternativa seleccionada:** Bases de datos independientes por microservicio.
- **Justificación:**
  * Aumenta la independencia de los microservicios.
  * Mejora la escalabilidad, ya que permite ajustar los recursos de cada microservicio según sus necesidades.

## Paso 5: Instanciar elementos arquitectónicos, asignar responsabilidades y definir interfaces
- Se agregan las siguientes bases de datos:
  * **Clientes:** Guarda toda la información personal de los clientes.
  * **Pedidos:** Almacena toda la información relacionada con los pedidos.
  * **Repartos y rutas:** Guarda toda la información relacionada con las rutas y repartos. 
  * **Pagos:** Almacena información sobre los pagos.
  * **Estadísticas:** Guarda todas las estadísticas calculadas a partir de los datos.
  * **Incidencias:** Guarda las incidencias ocurridas en el reparto.
- En etapas posteriores, se adoptarán estrategias para garantizar consistencia y sincronización entre las bases de datos de los microservicios.

## Paso 6: Esbozar vistas y registrar decisiones
- **Registro de decisiones:**
  * En el ADR2 se registra la decisión clave que es la incorporación de una base de datos para cada microservicio.

    [ADR2: Implementación de la persistencia de datos](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%202/ADR2-Implementaci%C3%B3n%20de%20la%20persistencia%20de%20datos.md)
    
- **Vista creada:**
  * Un diagrama de componentes mostrando la relación entre los microservicios y sus respectivas bases de datos.

    [Vista microservicios con DB](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%202/vista-microservicios-con-bases-de-datos.md)
    
## Paso 7: Realizar un análisis del diseño actual
- **Evaluación de la solución:**
  * Se validó que la descentralización mejora la escalabilidad, independencia y encapsulamiento.
- **Tradeoffs aceptados:**
  * **Tradeoff entre autonomía y complejidad:** Usar bases de datos independientes mejora la autonomía, pero requiere mecanismos adicionales para mantener la consistencia entre microservicios.
  * **Tradeoff entre independencia y costos iniciales:** Los microservicios con bases de datos propias ofrecen mayor independencia, pero aumentan los costos iniciales en infraestructura.
  * **Tradeoff entre escalabilidad y consistencia:** La descentralización facilita la escalabilidad, pero puede complicar la consistencia de datos entre microservicios.
- **Pendientes:**
  * Adoptar estrategias para garantizar consistencia y sincronización entre las bases de datos de los microservicios.

# Aplicación del Método ADD en la Iteración 3: Estrategia de Consistencia de Datos

## Paso 2: Establecer el objetivo de la iteración seleccionando los drivers

- **Drivers seleccionados:**
  * Escalabilidad.
  * Pendiente de la iteración anterior.
- **Objetivo de la iteración:** Implementar una estrategia de consistencia y sincronización entre las bases de datos de los microservicios.
  
## Paso 3: Seleccionar uno o más elementos del sistema a refinar

- **Elemento seleccionado:** El mecanismo de consistencia de datos entre microservicios.
- **Decisión:** Seleccionar una estrategia de consistencia y sincronización para las bases de datos de los microservicios.
  
## Paso 4: Elegir conceptos de diseño para satisfacer los drivers seleccionados
- **Alternativas evaluadas:**
  * Patrón Saga.
  * Interacción directa entre microservicios.
  * Event Sourcing.
- **Alternativa seleccionada:** Event Sourcing.
- **Justificación:**
  * Event Sourcing permite que cada microservicio mantenga su propio estado y los sincronice mediante eventos, asegurando la consistencia eventual sin afectar la escalabilidad.


## Paso 5: Instanciar elementos arquitectónicos, asignar responsabilidades y definir interfaces
- Se agregan los siguientes componentes:
  * **Bus de estadísticas:** Gestiona todos los eventos relacionados con las estadísticas.
  * **Event Store de estadísticas:** Almacena los eventos publicados en el bus de estadísticas.
  * **Bus de pedidos:** Gestiona todos los eventos relacionados con la realización de un nuevo pedido.
  * **Event Store de pedidos:** Almacena los eventos publicados en el bus de pedidos.
- En lugar de que los microservicios se comuniquen directamente entre sí, lo harán a través de eventos. Algunos microservicios publican eventos y otros microservicios reaccionan a los mismos.

## Paso 6: Esbozar vistas y registrar decisiones

- **Registro de decisiones:**
  * En el ADR3 se registra la decisión clave que es la implementación de una estrategia basada en Event Sourcing
  
    [ADR3: Estrategia de consistencia de datos](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%203/ADR3-Estrategia%20de%20consistencia%20de%20datos.md)
- **Vistas creadas:**
  * Un diagrama de componentes mostrando la relación entre los microservicios, los bus de estadísticas y pedidos con sus respectivas bases de datos.
  * Un diagrama de flujo mostrando los pasos de realizar un pedido, destacando cómo los eventos son generados, almacenados en el Event Store y distribuidos a través del sistema.
    
    [Vista Event Sourcing](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%203/vista-event-sourcing.md)

## Paso 7: Realizar un análisis del diseño actual
- **Evaluación de la solución:**
  * Se validó que el enfoque de Event Sourcing mejora la consistencia eventual entre los microservicios sin generar dependencias fuertes entre ellos, lo que favorece la escalabilidad.
- **Tradeoffs aceptados:**
  * **Tradeoff entre escalabilidad y consistencia:** La implementación de Event Sourcing mejora la escalabilidad, pero introduce complejidad en la gestión de la consistencia entre microservicios, requiriendo un esfuerzo adicional para garantizar que los eventos sean correctamente procesados y almacenados.
  * **Tradeoff entre desacoplamiento y complejidad operativa:** El uso de Event Sourcing reduce las dependencias directas entre microservicios, pero aumenta la complejidad operativa debido a la necesidad de gestionar los eventos, los Event Stores y las colas de mensajería.
  * **Tradeoff entre historial completo y almacenamiento adicional:** Aunque el Event Sourcing permite mantener un registro completo de todos los eventos, esto requiere almacenamiento adicional para guardar los eventos de cada microservicio, lo que incrementa los costos y la carga de gestión del sistema.

# Aplicación del Método ADD en la Iteración 4: Estrategia de Procesamiento Concurrente en la Gestión de Pedidos

## Paso 2: Establecer el objetivo de la iteración seleccionando los drivers

- **Drivers seleccionados:**
  * Performance.
  * Escalabilidad.
- **Objetivo de la iteración:** Implementar un sistema de procesamiento concurrente para los pedidos, garantizando que el sistema pueda manejar múltiples solicitudes simultáneamente.
  
## Paso 3: Seleccionar uno o más elementos del sistema a refinar

- **Elemento seleccionado:** El proceso secuencial de gestión de pedidos.
- **Decisión:** Implementar una estrategia de concurrencia entre pedidos de modo que cada uno pueda avanzar a través de las fases de manera independiente, sin esperar a que otros pedidos terminen.
  
## Paso 4: Elegir conceptos de diseño para satisfacer los drivers seleccionados

- **Alternativas evaluadas:**
  * Seguir con el procesamiento secuencial de pedidos.
  * Procesamiento concurrente de pedidos con balanceador de carga.
- **Alternativa seleccionada:** Procesamiento concurrente con un balanceador de carga.
- **Justificación :**
  * Al permitir la ejecución paralela de pedidos, el sistema puede manejar un volumen más alto de solicitudes.
  * La concurrencia permite procesar múltiples pedidos simultáneamente, reduciendo los tiempos de espera.

## Paso 5: Instanciar elementos arquitectónicos, asignar responsabilidades y definir interfaces

- Se agregan los siguientes componentes:
  * **Instancias del microservicio de Pedidos:** Procesan los pedidos de manera independiente, permitiendo que cada uno avance sin esperar a los demás.
  * **Balanceador de carga:** Distribuye las solicitudes entre las instancias del microservicio de pedidos de manera eficiente.

## Paso 6: Esbozar vistas y registrar decisiones

- **Registro de decisiones:**
  * En el ADR4 se registra la decisión clave de adoptar una estrategia de procesamiento concurrente, con la implementación de un balanceador de carga.
   
    [ADR4: Estrategia de Procesamiento Concurrente en la Gestión de Pedidos](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%204/ADR4-Estrategia%20de%20Procesamiento%20Concurrente%20en%20la%20Gesti%C3%B3n%20de%20Pedidos.md)
- **Vista creada:**
  * Se incluye un diagrama de componentes que muestra la relación entre el microservicio de clientes, el balanceador de carga, las instancias de microservicio de pedidos y la base de datos y el bus asociados.
  
    [Vista concurrencia en microservicio de pedido](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%204/vista-concurrencia-microservicio-pedidos.md)

## Paso 7: Realizar un análisis del diseño actual

- **Evaluación de la solución:**
  * Se validó que el procesamiento concurrente mejora la escalabilidad y reduce los tiempos de espera, permitiendo una mejor gestión de los pedidos.
- **Tradeoffs aceptados:**
  * **Tradeoff entre escalabilidad y latencia:** Aunque el balanceador de carga introduce una pequeña latencia, mejora significativamente la escalabilidad.
  * **Tradeoff entre costos iniciales y rendimiento:** Configurar y mantener un balanceador de carga y ajustar el sistema para manejar concurrencia puede implicar costos y esfuerzos iniciales.
  * **Tradeoff entre performance y complejidad:** El procesamiento paralelo mejora el rendimiento pero aumenta la complejidad operativa.

# Aplicación del Método ADD en la Iteración 5: Implementación de Seguridad Basada en Autenticación y Roles

## Paso 2: Establecer el objetivo de la iteración seleccionando los drivers

- **Drivers seleccionados:**
  * Seguridad.
  * Requerimientos Funcionales.
- **Objetivo de la iteración:** Implementar un sistema de seguridad basado en autenticación y roles, donde se definan roles específicos según las necesidades de cada usuario y su acceso a funcionalidades sensibles.

## Paso 3: Seleccionar uno o más elementos del sistema a refinar

- **Elemento seleccionado:** El control de acceso actual, que no tiene un control adecuado sobre los privilegios por usuario.
- **Decisión:** Implementar un sistema de autenticación y asignación de roles basado en los requerimientos funcionales del sistema. Esto garantiza que cada usuario acceda solo a los recursos y funcionalidades necesarios para su tarea.
  
## Paso 4: Elegir conceptos de diseño para satisfacer los drivers seleccionados

- **Alternativa seleccionada:** Control de acceso basado en autenticación y roles.
- **Justificación :**
  * Mejora la seguridad, garantizando que solo los usuarios autorizados tengan acceso a información sensible.
  * Garantiza que los usuarios se autentiquen correctamente antes de acceder al sistema.
    
## Paso 5: Instanciar elementos arquitectónicos, asignar responsabilidades y definir interfaces

- Se definen los siguientes roles según las necesidades de acceso a funcionalidades específicas:
  * **Clientes.**
  * **Administradores.**
  * **Gestores de rutas.**
    
- Cada rol tiene funcionalidades específicas que puede realizar dentro del sistema.

## Paso 6: Esbozar vistas y registrar decisiones

- **Registro de decisiones:**
  * En el ADR5 se registra la decisión clave de implementar un sistema de autenticación y roles para controlar el acceso a las funcionalidades del sistema.
 
    [ADR5: Implementación de Seguridad Basada en Autenticación y Roles](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%205/ADR5-Implementaci%C3%B3n%20de%20Seguridad%20Basada%20en%20Autenticaci%C3%B3n%20y%20Roles.md)
- **Vista creada:**
  * Una tabla que muestra los diferentes roles que puede tener un usuario y las funcionalidades correspondientes a cada rol.
 
    [Tabla de roles](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%205/tabla-roles.md)
    
## Paso 7: Realizar un análisis del diseño actual
- **Evaluación de la solución:**
Se validó que el sistema basado en roles mejora la seguridad y permite un control de acceso más efectivo, reduciendo la exposición a información sensible.
- **Tradeoffs aceptados:**
  * **Tradeoff entre seguridad y complejidad:** La implementación de roles introduce mayor complejidad en la gestión de usuarios, pero mejora la seguridad y el control de acceso.
  * **Tradeoff entre flexibilidad y costos:** Definir y gestionar roles de manera efectiva requiere esfuerzos adicionales, pero proporciona flexibilidad y escalabilidad en la administración de usuarios.

# Utilización de IA como asistente para la exploración y análisis de decisiones de diseño:
**Durante el desarrollo del trabajo utilizamos ChatGPT para lo siguiente:**
- Búsqueda de opciones que se podrían considerar para cada iteración.
- Ventajas y desventajas de las opciones consideradas.
