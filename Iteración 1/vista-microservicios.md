# Vista de microservicios del sistema

![vista-microservicios](https://github.com/user-attachments/assets/083f7ead-e02d-4914-af7e-5e7b79246cbb)

## Explicación:

### Microservicio de Clientes 
Maneja toda la información personal de los clientes (datos de contacto, dirección, historial de pedidos, etc.) y su autenticación. Se conecta con el sistema de pedidos para solicitar el catálogo, agregar, editar, eliminar, ver y finalizar pedidos.

### Microservicio de Pedidos
Gestiona la creación, procesamiento y seguimiento de pedidos. Se comunica con el microservicio de catálogo para acceder a los productos, con el microservicio de pagos para realizar el pago y con el microservicio de reparto y rutas para coordinar la entrega.

### Microservicio de Reparto y Rutas
Gestiona la asignación de rutas para los camiones de reparto y la asignación de flotas. Además, optimiza las rutas de acuerdo con los algoritmos de optimización. Se comunica con el microservicio de pedidos para recibir información sobre las entregas a realizar y con el de incidencias para informar algún problema con los repartos o los camiones.

### Microservicio de Pagos 
Gestiona la interacción con el sistema de pagos de MercadoLibre para procesar pagos de los clientes.

### Microservicio de Estadísticas
Recopila y proporciona estadísticas sobre el estado de los pedidos, la situación de los camiones de reparto, y datos de clientes. Recibe información de los microservicios de pedidos, reparto y de clientes.

### Microservicio de Incidencias
Gestiona el registro y seguimiento de incidencias en el reparto, como camiones averiados o entregas no realizadas. Recibe información del microservicio de reparto y rutas cuando hay problemas durante el proceso de entrega.

### API Gateway 
Se comunica con:
- el microservicio de estadísticas cuando la empresa las solicita.
- el microservicio de cliente  cuando un cliente quiere acceder a su cuenta y gestionarla.
- el microservicio de repartos y rutas cuando los gestores de rutas quieren gestionar el reparto de las flotas y las rutas de los camiones.
- el microservicio de incidencias cuando los gestores de ruta quieren ver las incidencias y gestionarlas.

### Mercado Libre
Servicio externo que proporciona servicios de pagos.
