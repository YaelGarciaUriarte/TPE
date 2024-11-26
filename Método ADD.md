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
