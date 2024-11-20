# ADR5: Implementación de Seguridad Basada en Autenticación y Roles

## Contexto y planteamiento del problema

En el sistema de la compañía de productos alimenticios, varios procesos críticos son gestionados a través de microservicios que interactúan con datos sensibles, como información personal de clientes y detalles de pagos. Actualmente, no existe un control adecuado sobre quién puede acceder a qué recursos por lo que surge la necesidad de garantizar un acceso seguro y restringido a esta información.


## Factores que impulsan la toma de decisiones


- Seguridad: los datos personales de los usuarios y la información de pago deben estar protegidos.

- Requerimientos Funcionales: La división de roles se basará en los requerimientos funcionales del sistema, asegurando que cada usuario tenga acceso únicamente a las funcionalidades requeridas para su tarea específica.


## Resultado de la decisión

Se implementará un sistema de seguridad basado en autenticación y roles, el cual garantiza que los usuarios se autentiquen correctamente antes de acceder al sistema, y se les asignen roles específicos según sus necesidades y responsabilidades dentro del sistema. Los roles se definirán según los requerimientos funcionales, garantizando que cada usuario acceda solo a las funciones y datos necesarios para su tarea.


## Consecuencias

### Ventajas:

- Control de acceso mejorado: Solo los usuarios con el rol adecuado tienen acceso a ciertas funcionalidades, lo que reduce el riesgo de accesos no autorizados.

- Protección de datos: Limita la exposición de datos sensibles al restringir el acceso según el rol del usuario.

- Flexibilidad para la gestión de usuarios: Permite asignar y modificar roles fácilmente según los cambios en las responsabilidades del usuario o en los requisitos del negocio, sin afectar la estructura general del sistema.

- Facilita la auditoría y el cumplimiento normativo: Tener roles bien definidos facilita el seguimiento y registro de las actividades de los usuarios, lo que es útil para auditorías de seguridad y cumplimiento de normativas.

### Desventajas:

- Complejidad en la gestión de roles: Definir y mantener roles adecuados para cada usuario puede volverse complejo a medida que el sistema crece.

- Costos adicionales de implementación y mantenimiento: Definir y gestionar roles de manera adecuada puede requerir esfuerzos adicionales en el diseño, desarrollo y mantenimiento del sistema de seguridad.
