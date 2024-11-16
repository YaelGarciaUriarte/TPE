# Vista Event Sourcing

![eventSourcing](https://github.com/user-attachments/assets/20cb01a6-bd8e-4809-8204-f571e55a1a3b)

## Descripción de los nuevos componentes:

### Bus de estadísticas

En lugar de comunicarse directamente con los microservicios de Pedidos, Cliente y Repartos y Rutas con Estadísticas, el bus de estadísticas permite que los mismos se comuniquen a través de eventos.
Los microservicios de Pedidos, Cliente y Repartos y Rutas publican los eventos (cambios en los datos del cliente, nuevo cliente, nuevos pedidos, situación de los camiones, etc ) y el microservicio de Estadísticas reacciona a ellos para actualizar las estadísticas.

### Event Store de estadísticas

Se almacenan los eventos publicados en el bus de estadísticas por los microservicios de Pedidos, Cliente y Repartos y Rutas.

### Bus de pedidos 

Gestiona todos los eventos relacionados con la realización de un nuevo pedido(pagos, transporte, etc).

### Event Store de pedidos

Se almacenan los eventos publicados en el bus de pedidos por los microservicios de Pedidos, Pagos y Repartos y Rutas.

# Eventos de realizar pedido:

![Eventos-pedidos](https://github.com/user-attachments/assets/34359316-04a5-416a-beb3-f999a888b8e6)

Pasos:

1.  El microservicio de Clientes solicita realizar un pedido al microservicio de Pedidos.
 
2. El microservicio de Pedidos publica un evento de pedido.

3. El evento de pedido se guarda en el Event Store y el microservicio de Pagos reacciona al evento para gestionar el pago.

4. El microservicio de Pagos publica un evento de pago OK.

5. El evento de pago OK se guarda en el Event Store. El microservicio de Pedidos reacciona al evento para guardar el estado de pago del pedido y el microservicio de Repartos y Rutas reacciona al evento para gestionar el reparto.

6. El microservicio de Repartos y Rutas publica un evento de reparto OK.

7. El evento de reparto OK se guarda en el Event Store y el microservicio de Pedidos reacciona al evento para guardar el estado de reparto del pedido.

