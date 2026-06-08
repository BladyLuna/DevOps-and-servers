# Comandos básicos de Docker

En esta sección guardo los comandos más importantes para empezar a usar Docker desde la terminal.

La idea es entender qué hace cada comando y cuándo usarlo.

---

## Verificar que Docker está instalado

```bash
docker --version
```

Este comando muestra la versión instalada de Docker.

También puedo usar:

```bash
docker info
```

Este comando muestra información más completa del sistema Docker, como contenedores, imágenes, versión del servidor, plugins y configuración.

---

## Probar Docker

```bash
docker run hello-world
```

Este comando descarga y ejecuta una imagen de prueba.

Sirve para comprobar que Docker funciona correctamente.

Si todo está bien, Docker mostrará un mensaje indicando que la instalación funciona.

---

## Descargar una imagen

```bash
docker pull nginx
```

Este comando descarga la imagen `nginx` desde Docker Hub.

Una imagen es como una plantilla para crear contenedores.

Otros ejemplos:

```bash
docker pull ubuntu
docker pull mysql
docker pull postgres
```

---

## Ver imágenes descargadas

```bash
docker images
```

Muestra las imágenes que tengo descargadas en mi máquina.

También se puede usar:

```bash
docker image ls
```

Ambos comandos sirven para listar imágenes.

---

## Ejecutar un contenedor

```bash
docker run nginx
```

Este comando crea y ejecuta un contenedor usando la imagen `nginx`.

Si la imagen no existe localmente, Docker la descarga automáticamente.

---

## Ejecutar un contenedor en segundo plano

```bash
docker run -d nginx
```

La opción `-d` significa `detached`.

Esto permite que el contenedor se ejecute en segundo plano y la terminal quede libre.

---

## Asignar un nombre al contenedor

```bash
docker run -d --name mi-nginx nginx
```

La opción `--name` permite darle un nombre personalizado al contenedor.

Esto ayuda a manejarlo más fácil después.

Ejemplo:

```bash
docker stop mi-nginx
docker start mi-nginx
```

---

## Mapear puertos

```bash
docker run -d -p 8080:80 nginx
```

La opción `-p` permite conectar un puerto de mi máquina con un puerto del contenedor.

En este ejemplo:

```text
8080:80
```

Significa:

```text
puerto_del_host:puerto_del_contenedor
```

Entonces puedo abrir en el navegador:

```text
http://localhost:8080
```

y ver el servidor Nginx que está corriendo dentro del contenedor.

---

## Ver contenedores activos

```bash
docker ps
```

Muestra solo los contenedores que están ejecutándose.

---

## Ver todos los contenedores

```bash
docker ps -a
```

Muestra todos los contenedores, incluso los detenidos.

---

## Detener un contenedor

```bash
docker stop nombre_del_contenedor
```

Ejemplo:

```bash
docker stop mi-nginx
```

También se puede detener usando el ID del contenedor:

```bash
docker stop 123abc
```

---

## Iniciar un contenedor detenido

```bash
docker start mi-nginx
```

Este comando vuelve a iniciar un contenedor que ya existe.

No crea uno nuevo.

---

## Reiniciar un contenedor

```bash
docker restart mi-nginx
```

Detiene y vuelve a iniciar el contenedor.

---

## Eliminar un contenedor

```bash
docker rm mi-nginx
```

Elimina un contenedor detenido.

Si el contenedor está activo, primero debo detenerlo:

```bash
docker stop mi-nginx
docker rm mi-nginx
```

O forzar la eliminación:

```bash
docker rm -f mi-nginx
```

---

## Eliminar una imagen

```bash
docker rmi nginx
```

Elimina una imagen descargada.

También se puede usar el ID de la imagen:

```bash
docker rmi image_id
```

Si una imagen está siendo usada por un contenedor, primero debo eliminar el contenedor.

---

## Ver logs de un contenedor

```bash
docker logs mi-nginx
```

Muestra la salida o registros del contenedor.

Para seguir viendo los logs en tiempo real:

```bash
docker logs -f mi-nginx
```

---

## Entrar a un contenedor

```bash
docker exec -it mi-nginx sh
```

Este comando abre una terminal dentro del contenedor.

Partes importantes:

```text
exec -> ejecuta un comando dentro del contenedor
-it  -> modo interactivo
sh   -> shell del contenedor
```

En algunas imágenes se puede usar `bash`:

```bash
docker exec -it nombre_contenedor bash
```

Pero en imágenes pequeñas como `nginx:alpine`, normalmente se usa `sh`.

---

## Ver información detallada de un contenedor

```bash
docker inspect mi-nginx
```

Muestra información completa del contenedor, como:

- IP interna
- red
- volúmenes
- puertos
- configuración
- variables de entorno

---

## Ver uso de recursos

```bash
docker stats
```

Muestra el uso de CPU, memoria y red de los contenedores activos.

---

## Ver procesos dentro de un contenedor

```bash
docker top mi-nginx
```

Muestra los procesos que están corriendo dentro del contenedor.

---

## Limpiar contenedores detenidos

```bash
docker container prune
```

Elimina contenedores detenidos.

Docker pedirá confirmación antes de borrar.

---

## Limpiar imágenes no utilizadas

```bash
docker image prune
```

Elimina imágenes que no están siendo utilizadas.

---

## Limpiar recursos no utilizados

```bash
docker system prune
```

Elimina recursos que Docker ya no está usando, como:

- contenedores detenidos
- redes no usadas
- imágenes colgantes
- caché de build

Usar con cuidado.

---

# Ejemplo práctico con Nginx

Levantar un servidor Nginx:

```bash
docker run -d --name web-nginx -p 8080:80 nginx
```

Verificar que está corriendo:

```bash
docker ps
```

Abrir en el navegador:

```text
http://localhost:8080
```

Ver logs:

```bash
docker logs web-nginx
```

Entrar al contenedor:

```bash
docker exec -it web-nginx sh
```

Detenerlo:

```bash
docker stop web-nginx
```

Eliminarlo:

```bash
docker rm web-nginx
```

---

# Resumen rápido

| Comando | ¿Para qué sirve? |
|---|---|
| `docker --version` | Ver versión de Docker |
| `docker info` | Ver información del sistema Docker |
| `docker run hello-world` | Probar Docker |
| `docker pull nginx` | Descargar una imagen |
| `docker images` | Ver imágenes |
| `docker run nginx` | Crear y ejecutar un contenedor |
| `docker run -d nginx` | Ejecutar en segundo plano |
| `docker run -p 8080:80 nginx` | Mapear puertos |
| `docker ps` | Ver contenedores activos |
| `docker ps -a` | Ver todos los contenedores |
| `docker stop nombre` | Detener un contenedor |
| `docker start nombre` | Iniciar un contenedor detenido |
| `docker restart nombre` | Reiniciar un contenedor |
| `docker rm nombre` | Eliminar un contenedor |
| `docker rmi imagen` | Eliminar una imagen |
| `docker logs nombre` | Ver logs |
| `docker exec -it nombre sh` | Entrar a un contenedor |
| `docker inspect nombre` | Ver información detallada |
| `docker stats` | Ver uso de recursos |
| `docker system prune` | Limpiar recursos no usados |

---

# Nota personal

Los comandos más importantes al inicio son:

```bash
docker ps
docker ps -a
docker images
docker run
docker stop
docker rm
docker logs
docker exec -it
```

Con esos comandos ya puedo empezar a crear, revisar, detener y eliminar contenedores.
