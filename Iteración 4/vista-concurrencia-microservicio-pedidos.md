# Vista concurrencia microservicio pedidos

![Concurrencia-Microservicio-Pedidos](https://github.com/user-attachments/assets/11d9d25d-ca69-41b3-b8a2-167db8de5802)

# Descripción de los componentes:

## Microservicio Clientes

Envía los pedidos para que sean procesados.

## Balanceador de carga

Distribuye las solicitudes de manera eficiente entre los diferentes nodos de procesamiento.

## Instancias de microservicio de Pedidos 
Procesan pedidos de manera independiente, permitiendo que cada pedido avance por sus fases sin dependencia de otros.

*Como ejemplo, se incluyen 3 instancias del microservicio de pedidos pero la cantidad real de instancias deberá ajustarse según la carga de trabajo esperada.*

## Base de Datos y Bus de Pedidos

Ambos centralizan y sincronizan la información de pedidos, asegurando persistencia y un flujo adecuado de datos.
