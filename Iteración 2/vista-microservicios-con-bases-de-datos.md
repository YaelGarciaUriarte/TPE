# Vista de microservicios del sistema con bases de datos

![vista-microservicios](https://github.com/user-attachments/assets/8a9822fb-3eeb-47c9-aca7-4c3de4359678)

## Explicación:

### Base de Datos de Clientes
Guarda toda la información personal de los clientes (datos de contacto, dirección, historial de pedidos, etc.) y su autenticación. Se consulta cuando se quieren obtener los mismos.

### Base de Datos de Pedidos
Almacena toda la información relacionada con los pedidos (pedidos realizados, pedidos en proceso, etc). Se lee cuando el microservicio de estadísticas solicita información.

### Base de Datos Reparto y Rutas
Guarda toda la información relacionada con las rutas para los camiones de reparto, la asignación de flotas y el historial de repartos. Se lee cuando el gestor de rutas o el microservicio de estadísticas solicitan información.

### Base de Datos  de Pagos
Almacena información sobre los pagos y se lee cuando se quiere consultar sobre un pago de algún pedido.

### Base de Datos de Estadísticas
Guarda todas las estadísticas calculadas a partir de los datos y se lee cuando alguien las solicita.


### Base de Datos de Incidencias
Guarda las incidencias ocurridas en el reparto, como camiones averiados o entregas no realizadas. Se lee cuando el gestor de rutas las solicita.
