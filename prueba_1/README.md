Diagrama AWS:

Se generó el siguiente diagrama con el objetivo de dar soporte a los siguientes puntos requeridos:

- Cargas variables
- Contar con HA (alta disponibilidad)
- Frontend en Js
- Backend con una base de datos relacional y una no relacional
- La aplicación backend consume 2 microservicios externos

Cargas variables: Para que la aplicación pueda soportar una división en la carga de datos, se estableció crear dentro de la misma VPC un Balanceador de carga y un grupo de auto-scaling. 
El balanceador de carga va a distribuir las solicitudes de acuerdo al tráfico y procesamiento.
El grupo de auto-scaling va a servir para crecer o reducir los números de instancias de acuerdo a la demana.

Alta Disponibilidad: Para aumentar la tolerancia a fallos, se estimó escalar horizontalmente entre dos zonas de disponibilidad dentro de una misma región. 

FrontEnd en JS: Se crearan dos instancias de EC2 t2.micro con una imagen de Ubuntu 20.04 donde se podrán instalar las dependencias para correr la app.

Backend: Para resolver la conexion a dos bases de datos diferentes y mantener la alta disponibilidad se resolvió:
Base de datos relacional: Se utilizará el servicio de RDS para levantar un motor de BD MySQL con disponibilidad Multi-AZ, lo que produce que se copien todos los datos en una BD secudaria dentro de una segunda AZ para mantener una replica en stand-by. Si la BD primaria falla, las solicitudes se redireccionan a la BD secundaria en Stand-by.
Base de datos no relacional: Debido a que DynamoDB se configura fuera de la VPC, se configuró un punto de enlace para conectar mediante IP privada la VPC y la BD. De este modo, se evita salir a Internet para conectar con la BD de amazon y asi proteger los datos.

Microservicios: Se configura un gateway para consumir datos de Internet, en este caso, microservicios como por ejemplo API's de terceros.ß	