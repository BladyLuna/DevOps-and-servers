## 📦 Contenedores

docker ps # ver contenedores activos  
docker ps -a # ver TODOS (incluye apagados)

docker run # crear y ejecutar contenedor  
docker start ID # iniciar contenedor  
docker stop ID # detener contenedor  
docker restart ID # reiniciar

docker rm ID # eliminar contenedor

## 🧠 Ejemplo real

docker run -d -p 8000:8000 nginx

👉 crea un contenedor con Nginx
