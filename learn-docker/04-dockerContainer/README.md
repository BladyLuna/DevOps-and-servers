# Docker Container

- una instancia en ejecucion de una imagen
- puedes encontrar muchisimas imagenes en docker.hub(repositorio de contenedores)
- logra el rendimiento del sistema operativo
- puede aver varios contenedores en una sola maquina

  <img src="../img/dockerContainers.png" width="300" height="200">

apartir de una imagen podemos ejecutar varios contenedores... cada contenedor tiene un ID unico, y tienen un rendimiento nativo

### Comandos

1. para ver la lista de contenedores que se estan ejecutando

```bash
docker ps
```

2. ver todos los contenedores ejecutados

```bash
docker ps -a
docker ps -aq
```

3. los comandos basicos

```bash
docker run         # crear y ejecutar contenedor
docker start ID    # iniciar contenedor
docker stop ID     # detener contenedor
docker restart ID  # reiniciar

docker rm ID       # eliminar contenedor
```

4. eliminar todos los contenedores

```bash
docker rm $(docker rm -aq)
```

# ejemplos con servidores

que son son los volion -v es que puedes agregar un archivo deste los parametros de docker para mostrarlo
eejemplo 1 con nginx

```bash
docker ps -a
docker pull nginx
# puedes ejecutar el mismo contenedor en diferentes puerto por que serian diferentes contenedores o ISOS
docker run -p : 80:80 -d nginx # ir al navegador localhost 80
# muchos puertos a la ves
docker rum -p 8000:80 -p 4000:80 -p 6000:80 -d nginx
docker stop nginx
```

paara agregarle contenido al servidor

```bash
docker run -d -p 80:80 --name website -v $(pwd):/usr/share/nginx/html:ro nginx
# la propiedad ro -> read only no te deja acceder a la bash de l servidor , primreo para el srvidor
docker exec -it website bash
```

ejemplo 2 con APACHE

```bash
docker run -p 3300:80 -d httdp
```

ejemplo 3 con MYSQL revisar la imagen en docker hub

```bash
# tiene nombre
docker run -p -d 3306:3306 --name mydatabase mysql
# para accder a mysql
docker exec -it laravel_db mysql -u root -p
docker run -p -d 3306:3306 --name -e MYSQL_ROOT_PASSWORD=conrtasena mydatabase mysql
```

### docker formats

para mostrar con formato mas limpio

```bash
# este es el string DOCKER_FORMAT (pueden agregar a su archivo bashrc, .zshrc, etc):
export DOCKER_FORMAT="ID\t{{.ID}}\nNAME\t{{.Names}}\nPORT\t{{.Ports}}\nStatu    s\t{{.Status}}\nCOMMAND\t{{.Command}}\nCREATED\t{{.CreatedAt}}\nSize\t{{.Size}}\n"
```

5. todo esto se puede reemplazar por docker files 
