# TPE: Diseño de Sistemas de Software

Este proyecto contiene una arquitectura propuesta para una compañía de productos alimenticios.

### Miembros del equipo:

- Danderfer Julieta
  
- Garcia Uriarte Yael
  
Contacto del equipo: 

- jdanderfer@alumnos.exa.unicen.edu.ar

- ygarciauriarte@alumnos.exa.unicen.edu.ar

## Sistema de Gestión de Pedidos Basado en Microservicios

### Actores
- [Actores](https://github.com/YaelGarciaUriarte/TPE/blob/main/Requerimientos/Stakeholders.md)

### Requerimientos

Esta sección detalla los requerimientos extraídos del enunciado.

- [Requerimientos Funcionales](https://github.com/YaelGarciaUriarte/TPE/blob/main/Requerimientos/RequerimientosFuncionales.md)
  
- [Atributos de Calidad](https://github.com/YaelGarciaUriarte/TPE/blob/main/Requerimientos/AtributosDeCalidad.md)
  
### ADR

Los ADR vinculados a continuación registran las principales decisiones de arquitectura con respecto al diseño propuesto, incluido su contexto, justificación y el diagrama asociado a la decision.

#### [ADR1: División de funcionalidades en microservicios](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%201/ADR1-Divisi%C3%B3n%20de%20funcionalidades%20en%20microservicios.md)
-  [Vista microservicios](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%201/vista-microservicios.md)
#### [ADR2: Implementación de la persistencia de datos](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%202/ADR2-Implementaci%C3%B3n%20de%20la%20persistencia%20de%20datos.md)
-  [Vista microservicios con DB](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%202/vista-microservicios-con-bases-de-datos.md)
#### [ADR3: Estrategia de consistencia de datos](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%203/ADR3-Estrategia%20de%20consistencia%20de%20datos.md)
-  [Vista Event Sourcing](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%203/vista-event-sourcing.md)
#### [ADR4: Estrategia de Procesamiento Concurrente en la Gestión de Pedidos](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%204/ADR4-Estrategia%20de%20Procesamiento%20Concurrente%20en%20la%20Gesti%C3%B3n%20de%20Pedidos.md)
-  [Vista concurrencia en microservicio de pedido](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%204/vista-concurrencia-microservicio-pedidos.md)
#### [ADR5: Implementación de Seguridad Basada en Autenticación y Roles](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%205/ADR5-Implementaci%C3%B3n%20de%20Seguridad%20Basada%20en%20Autenticaci%C3%B3n%20y%20Roles.md)
-  [Tabla de roles](https://github.com/YaelGarciaUriarte/TPE/blob/main/Iteraci%C3%B3n%205/tabla-roles.md)

