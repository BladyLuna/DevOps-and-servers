# ¿Qué es Docker?

Docker es una plataforma que permite crear, ejecutar y administrar aplicaciones dentro de **contenedores**.

Un contenedor es un entorno ligero y aislado que incluye lo necesario para ejecutar una aplicación, como:

- código
- dependencias
- librerías
- configuración
- variables de entorno

La idea principal de Docker es que una aplicación pueda funcionar de forma similar en diferentes entornos:

- computadora local
- servidor
- máquina virtual
- nube
- entorno de producción

---

## Problema que resuelve Docker

Antes de Docker era común escuchar:

> "En mi máquina sí funciona."

Esto pasaba porque cada equipo podía tener diferentes versiones de:

- sistema operativo
- librerías
- dependencias
- configuraciones
- versiones de lenguajes

Docker ayuda a reducir ese problema empaquetando la aplicación y sus dependencias dentro de una imagen.

---

## Conceptos principales

### Imagen

Una imagen es una plantilla que contiene todo lo necesario para crear un contenedor.

Ejemplo:

```bash
docker pull nginx
```

---

### Contenedor

Un contenedor es una instancia en ejecución de una imagen.

Ejemplo:

```bash
docker run nginx
```

---

### Dockerfile

Un `Dockerfile` es un archivo con instrucciones para construir una imagen personalizada.

Ejemplo:

```Dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

---

### Docker Hub

Docker Hub es un registro público donde se almacenan imágenes listas para usar.

Ejemplos:

- nginx
- mysql
- postgres
- redis
- ubuntu
- node

---

## Docker vs Máquina virtual

| Característica | Docker | Máquina virtual |
|---|---|---|
| Peso | Ligero | Pesado |
| Arranque | Rápido | Más lento |
| Sistema operativo | Comparte el kernel del host | Tiene sistema operativo completo |
| Uso típico | Aplicaciones y servicios | Sistemas completos |
| Consumo de recursos | Menor | Mayor |

---

## ¿Para qué se usa Docker?

Docker se usa para:

- crear entornos de desarrollo
- levantar servidores web
- probar aplicaciones
- ejecutar bases de datos
- desplegar servicios
- crear laboratorios
- automatizar despliegues

---

## Comandos iniciales

Ver la versión de Docker:

```bash
docker --version
```

Probar que Docker funciona:

```bash
docker run hello-world
```

Listar contenedores activos:

```bash
docker ps
```

Listar todos los contenedores:

```bash
docker ps -a
```

Listar imágenes descargadas:

```bash
docker images
```

---

## Resumen

Docker permite ejecutar aplicaciones en contenedores ligeros, portables y aislados.

Su principal ventaja es que ayuda a mantener entornos consistentes entre desarrollo, pruebas y producción.
