# Docker Image

- es una plantilla para crear un entorno
- contiene todos los elementos necesarios para tu aplicacion(bibliotecas, entornos, archivos de configuracion,software , codigo, etc.)
- puede tener una version o instantaneas basadas en el tiempo, osea puedes descargar versiones anteriores de alguna tecnologia
- estas imagenes se crean usando una dockerFile
  <img src="../img/dockerImage.png" width="300" height="200">

## comandos

1. ver las imagenes que tengo instaladas

```bash
docker images
```

2. para ver las imagenes de docker hub en la terminal

```bash
docker shearch ubuntu
```

3. para decargar la imagen

```bash
docker pull name-Image
```

4. iniciar la imagen

```bash
docker run name-Image
```

5. para acceder o entrar a la imagen en este caso ubuntu

```bash
docker run -it name-Images bash
# it  -> iterativa
# bash -> aceso a la terminal
```

6. apartir de la imagenes se crean contenedores es decir , una imagen sirve para crear varios contenedore con diferentes ID, ejecutando un contenedor dentro de otro

```bash
# para ver los contenedores
docker ps

```

7. eliminar imagenes
   ```bash
   docker rmi ID
   # es como una subconsulta mysql XD
   docker rmi $(docker images -aq) -f

   ```
