# ADR4: Estrategia de Procesamiento Concurrente en la Gestión de Pedidos

## Contexto y planteamiento del problema

El sistema actual procesa los pedidos de manera secuencial, pasando por tres fases clave: preprocesado, autorización y aceptación. Para que un pedido avance a la siguiente fase, debe completarse correctamente la fase anterior. Esto significa que cada pedido debe esperar a que el anterior termine antes de comenzar su procesamiento, lo que limita la capacidad del sistema para gestionar múltiples pedidos concurrentemente, reduciendo su eficiencia y escalabilidad.



## Factores que impulsan la toma de decisiones


- Performance: el acceso a la base de datos y el uso de la aplicación por parte de los clientes debe generar respuestas rápidas.
  
- Escalabilidad: El sistema debe atender un número cada vez mayor de pedidos por hora.


## Resultado de la decisión

Se implementará una estrategia de concurrencia entre pedidos, permitiendo la ejecución paralela de múltiples pedidos, de modo que cada uno pueda avanzar a través de las fases de preprocesado, autorización y aceptación de manera independiente, sin esperar a que otros pedidos terminen.

Para gestionar eficientemente las solicitudes concurrentes y asegurar que el sistema no se sobrecargue, se implementará un balanceador de carga que distribuirá las solicitudes entre los diferentes procesos de pedidos, mejorando la escalabilidad y el rendimiento general del proceso.


## Consecuencias

### Ventajas:

- Escalabilidad Mejorada: combinado con un balanceador de carga, es fácil escalar horizontalmente al agregar más instancias del microservicio para manejar mayores volúmenes de tráfico.

- Tiempos de Respuesta Reducidos: la concurrencia permite procesar múltiples solicitudes al mismo tiempo, reduciendo los tiempos de espera.

- Distribución Uniforme de la Carga: el balanceador de carga asegura que las solicitudes se distribuyan equitativamente entre las instancias disponibles, evitando que una sola instancia se sature.

- Mayor Disponibilidad: si una instancia falla, el balanceador de carga redirige automáticamente las solicitudes a las instancias disponibles, garantizando continuidad en el servicio.

### Desventajas:

- El balanceador de carga introduce una pequeña latencia adicional al redirigir solicitudes y mantener la monitorización de las instancias.

- Configurar un balanceador de carga y ajustar el sistema para manejar concurrencia puede requerir tiempo y costos iniciales significativos.

- Si la demanda es baja, puedes terminar con recursos casi no utilizados debido a la configuración de múltiples instancias y un balanceador.
