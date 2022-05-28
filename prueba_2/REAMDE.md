Despliegue de aplicación multi-imagen:

Se pensaron dos soluciones para este inconveniente, uno utilizando docker compose y otro kubernetes.

Solución docker-compose: Dentro de las carpetas backend/frontend se crearon archivos de Dockerfile que compilan los repositorios.

Nota: El backend tuvo que ser tocado en los archivos de requirements debido a que muchos repositorios y dependencias estaban deprecados. Tambien, el archivo manage.py contiene una validación de SECRET_KEY, que se tuvo que pasar por variable de entorno generando una nueva a través de Djecrety.

Por ultimo, se creó un archivo de docker-compose que despliega dentro de su network las dos imágenes anteriormente mencionadas, exponiendo sus puertos a un gateway dentro de la red de docker-compose con salida a internet en la ip 192.168.0.1.

Ejecucion: Con "docker-compose up -d" se puede correr y ver los contenedores activos.


Solución Kubernetes: Para levantar estas imagenes en un cluster de K8s dentro de un proveedor de servicios se generaron 3 archivos:
*Namespace: craftechns
*Deployment: Este levanta una imagen exportada a DockerHub que pesa la mitad de espacio que utilizar dos imagenes separadas ya que se montaron las imagenes de django(python) y node utilizando un alias ("as builder") y un COPY --from=builder.

Ejecucion (teniendo los 3 archivos juntos): kubectl apply -f .