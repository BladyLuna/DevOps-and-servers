# Dockerfile

Un Dockerfile es un archivo con **instrucciones para crear una imagen** de Docker,
la cual luego se utiliza para ejecutar contenedores.
Estas instrucciones definen qué debe tener la imagen, como el sistema base,
las dependencias, archivos y comandos que se ejecutarán cuando se cree
un contenedor a partir de ella.

1. genera la imagen segun la instruciones del dockerfile
```bash
docker build -t test .
``` 
2.  ahora para ejercutar esta imagen creada
```bash
docker run -p 3000:80 -d --name testApp test
# testApp -> es el nombre del contenedor
# test -> es el nombre de la imagen
```

## subir tus imagenes ISOS  a docker hub
necesario crear cuenta de docker hub se usa el user name
```bash
#necesario logquearse
docker login 
docker run build -t BladyLuna/test .
docker push BladyLuna/test
```