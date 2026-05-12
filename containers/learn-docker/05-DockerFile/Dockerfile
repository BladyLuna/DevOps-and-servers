# el docker file es un paso a paso de lo que deberia hacer mi imagen para que funcione en cualquier sistema

FROM nginx:latest
#se especidica la imagen base a usar
# lasted para la ultima version de nginx pero tambien se puede especificar una version concreta como en este caso
WORKDIR /usr/share/nginx/html

COPY . . 
#copia los archivos de tu ruta actual dentro del contenedor
