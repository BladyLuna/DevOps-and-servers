# Docker Containers

Un contenedor de Docker es una instancia en ejecución de una imagen.
  <img src="../img/dockerContainers.png" width="300" height="200">

La imagen es la plantilla.  
El contenedor es la imagen ejecutándose.

A partir de una misma imagen puedo crear varios contenedores. Cada contenedor tiene:

- ID único
- nombre
- estado
- puertos
- logs
- configuración propia

Docker Hub no almacena contenedores, almacena imágenes que luego puedo descargar y ejecutar.

---

## Imagen vs Contenedor

```text
Imagen nginx  ->  contenedor nginx1
Imagen nginx  ->  contenedor nginx2
Imagen nginx  ->  contenedor nginx3
```

Todos pueden usar la misma imagen, pero cada contenedor funciona de manera independiente.

---

## Ver contenedores activos

```bash
docker ps
```

Muestra solo los contenedores que están en ejecución.

---

## Ver todos los contenedores

```bash
docker ps -a
```

Muestra todos los contenedores, incluso los detenidos.

Para mostrar solo los IDs:

```bash
docker ps -aq
```

---

## Comandos básicos para contenedores

Crear y ejecutar un contenedor:

```bash
docker run nginx
```

Crear y ejecutar en segundo plano:

```bash
docker run -d nginx
```

Crear con nombre:

```bash
docker run -d --name web nginx
```

Iniciar un contenedor detenido:

```bash
docker start web
```

Detener un contenedor:

```bash
docker stop web
```

Reiniciar un contenedor:

```bash
docker restart web
```

Eliminar un contenedor detenido:

```bash
docker rm web
```

Eliminar un contenedor aunque esté activo:

```bash
docker rm -f web
```

---

## Eliminar todos los contenedores

```bash
docker rm $(docker ps -aq)
```

Si algunos están activos, puedo forzar la eliminación:

```bash
docker rm -f $(docker ps -aq)
```

Usar con cuidado porque elimina todos los contenedores.

---

# Ejemplo 1: Nginx

Descargar imagen:

```bash
docker pull nginx
```

Ejecutar Nginx en el puerto 80:

```bash
docker run -d --name nginx-web -p 80:80 nginx
```

Abrir en el navegador:

```text
http://localhost
```

Ejecutar Nginx en otro puerto:

```bash
docker run -d --name nginx-web-8080 -p 8080:80 nginx
```

Abrir:

```text
http://localhost:8080
```

---

## Ejecutar varios contenedores con la misma imagen

```bash
docker run -d --name nginx1 -p 8000:80 nginx
docker run -d --name nginx2 -p 4000:80 nginx
docker run -d --name nginx3 -p 6000:80 nginx
```

Cada contenedor usa la imagen `nginx`, pero cada uno tiene diferente nombre y diferente puerto.

---

## Agregar contenido con volumen

Puedo montar una carpeta local dentro del contenedor usando `-v`.

Ejemplo:

```bash
docker run -d \
  --name website \
  -p 8080:80 \
  -v $(pwd):/usr/share/nginx/html:ro \
  nginx
```

Explicación:

```text
-v $(pwd):/usr/share/nginx/html:ro
```

Significa:

```text
carpeta_local:carpeta_del_contenedor:modo
```

`ro` significa `read only`, es decir, el contenedor solo puede leer los archivos.

Esto sirve para mostrar mi propio `index.html` usando Nginx.

---

## Entrar a un contenedor

```bash
docker exec -it website bash
```

Si la imagen no tiene `bash`, puedo usar:

```bash
docker exec -it website sh
```

---

# Ejemplo 2: Apache

Apache usa la imagen oficial llamada `httpd`.

```bash
docker run -d --name apache-web -p 3300:80 httpd
```

Abrir en el navegador:

```text
http://localhost:3300
```

---

# Ejemplo 3: MySQL

Para MySQL es necesario definir una contraseña para el usuario root.

```bash
docker run -d \
  --name mydatabase \
  -e MYSQL_ROOT_PASSWORD=contrasena \
  -p 3306:3306 \
  mysql
```

Entrar al cliente MySQL dentro del contenedor:

```bash
docker exec -it mydatabase mysql -u root -p
```

Docker pedirá la contraseña:

```text
contrasena
```

---

# Formato personalizado para docker ps

Puedo crear una variable para mostrar la salida de `docker ps` de forma más limpia.

```bash
export DOCKER_FORMAT="ID\t{{.ID}}\nNAME\t{{.Names}}\nPORT\t{{.Ports}}\nSTATUS\t{{.Status}}\nCOMMAND\t{{.Command}}\nCREATED\t{{.CreatedAt}}\nSIZE\t{{.Size}}\n"
```

Luego puedo usar:

```bash
docker ps --format "$DOCKER_FORMAT"
```

Si quiero guardar esta variable permanentemente, la puedo agregar a:

```bash
~/.bashrc
```

o:

```bash
~/.zshrc
```

---

# Resumen rápido

| Comando | Función |
|---|---|
| `docker ps` | Ver contenedores activos |
| `docker ps -a` | Ver todos los contenedores |
| `docker ps -aq` | Ver solo IDs |
| `docker run nginx` | Crear y ejecutar contenedor |
| `docker run -d nginx` | Ejecutar en segundo plano |
| `docker run -d --name web nginx` | Crear contenedor con nombre |
| `docker start web` | Iniciar contenedor detenido |
| `docker stop web` | Detener contenedor |
| `docker restart web` | Reiniciar contenedor |
| `docker rm web` | Eliminar contenedor |
| `docker rm -f web` | Forzar eliminación |
| `docker exec -it web bash` | Entrar al contenedor |
| `docker logs web` | Ver logs |

---

# Nota personal

Un contenedor es una imagen en ejecución.

Puedo crear muchos contenedores desde una sola imagen.  
Lo importante es controlar:

- nombre
- puerto
- volumen
- variables de entorno
- estado del contenedor

Más adelante todo esto se puede automatizar mejor usando `Dockerfile` y `docker compose`.
