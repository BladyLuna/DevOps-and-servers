## Que es SSH?
secure shell es el significado , sirve para conectarse y autenticarte remotamente a servidores o servicios remotamente, puedes usar claves ssh para para confirmar confirmaciones de codigo.
### Acerca de las claves ssh 
puedes usar tu clave ssh para realisar operaciones de git atraves de ssh, y tambien con otros servicios
### Comprobando si existen claves SSH
- debes generar una clave SSH asegunrandote que no exista otra clave

Nota

GitHub mejoró la seguridad eliminando los tipos de claves antiguos e inseguros el 15 de marzo de 2022.

A partir de esa fecha, las claves DSA ( `ssh-dss`) ya no son compatibles. No puedes agregar nuevas claves DSA a tu cuenta personal en GitHub.

Las claves RSA ( `ssh-rsa`) con fecha `valid_after`anterior al 2 de noviembre de 2021 pueden seguir utilizando cualquier algoritmo de firma. Las claves RSA generadas después de esa fecha deben utilizar el algoritmo de firma SHA-2. Algunos clientes antiguos podrían necesitar una actualización para poder utilizar firmas SHA-2.


1. abrir la terminal
2. introdusca "ls -al ~/.ssh" para comprobar si existen claves ssh
```
$ ls -al ~/.ssh
# Lists the files in your .ssh directory, if they exist
```
3. consulata  un listado de directorios para ver si ya tienes una clave SSH , por defecto los nombres de los archivos de las claves compatibles con github son los siguientes

- _id_rsa.pub_
    
- _id_ecdsa.pub_
    
- _id_ed25519.pub_
4. Genera una nueva clave SSH o sube una clave existente 
- si no tiene disponibles claves SSH o no quiere usar las que tiene puede generar otras claves
- Si ve un par de claves pública y privada ya existente (por ejemplo, id_rsa.pub e id_rsa ) que le gustaría usar para conectarse a GitHub, puede agregar la clave al agente ssh
# Generar una nueva clave SSH y anadirla al agente SSH
## Acerca de las contrasenas de las claves SSH
puedes escribir y acceder a los datos en repositorios git media SSH te autenticas con la clave privada de tu equipo local.
Al generar una clave SSH, puedes agregar una contrasena para mayor seguridad. 
puede agregar al agente SSH . el agente SSH administra sus claves SSH y recuerda sus contrasena.
## Generacion de una nueva clase SSH
puedes generar una clave SSH en tu dispositivo local luego puedes anadirlo a tu cuenta GitHub para habilitar la autenticaciones de las operaciones atraves de SSH en github.
#### pasos:
1. abrir tu terminal
2. pega el siguiente bash replasandolo por tu correo electronico con el que usas github

```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
```
Nota

Si está utilizando un sistema heredado que no admite el algoritmo Ed25519, utilice:

```shell
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
siga los pasos leyendo.
3.  cuando te solicite una contrasena segura , agregue su contrasena segura
```shell
    > Enter passphrase (empty for no passphrase): [Type a passphrase]
    > Enter same passphrase again: [Type passphrase again]
```
4. las claves SSH se guardan en esta ruta
```shell
> Enter a file in which to save the key (/home/YOU/.ssh/id_ALGORITHM):[Press enter]
```

## Agregamos las claves SSH a un agente SSH
Antes de agregar debes haber hecho los otros pasos:
#### pasos:
1. iniciar el agente SSH en segundo plano

```shell
$ eval "$(ssh-agent -s)"
> Agent pid 59566
```
esto depende a tu entorno, preguntale a chatgpt xd.
2. agregue su clave privada SSH al agente SSH
si creo su clave privada con un nombre diferente, o si estas agregando una clave existente que tiene nombre diferente, reemplaze el id_ed56758 en el comando con el nombre del archivo.
```shell
ssh-add ~/.ssh/id_ed25519
```

-- ignorar
### Generacion de una nueva clave SSH para una clave de seguridad de hardware

1. Inserta la llave de seguridad de tu ordenador.
    
2. Abrir terminal .
    
3. Pega el texto que aparece a continuación, sustituyendo la dirección de correo electrónico del ejemplo por la dirección de correo electrónico asociada a tu cuenta de GitHub.
    
    ```shell
    ssh-keygen -t ed25519-sk -C "your_email@example.com"
    ```
    
    Nota
    
    Si el comando falla y recibe el error `invalid format`, `feature not supported,`es posible que esté utilizando una llave de seguridad de hardware que no sea compatible con el algoritmo Ed25519. Introduzca el siguiente comando en su lugar.
    
    ```shell
    ssh-keygen -t ecdsa-sk -C "your_email@example.com"
    ```
    
4. Cuando se le solicite, pulse el botón de su llave de seguridad física.
    
5. Cuando se le solicite que introduzca un archivo donde guardar la clave, pulse Intro para aceptar la ubicación de archivo predeterminada.
    
    ```shell
    > Enter a file in which to save the key (/home/YOU/.ssh/id_ed25519_sk):[Press enter]
    ```
    
6. Cuando se le solicite que escriba una contraseña, pulse **Intro** .
    
    ```shell
    > Enter passphrase (empty for no passphrase): [Type a passphrase]
    > Enter same passphrase again: [Type passphrase again]
    ```
    

# Agregar una nueva clave SSH a tu cuenta de github 
### Acerca de la adicion de claves SSH a su cuenta
Una vez que hayas generado un par de claves SSH, debes agregar la clave pública a GitHub.com para habilitar el acceso SSH a tu cuenta.
### Agregar una nueva clave SSH a su cuenta

1. Copia la clave pública SSH al portapapeles.
Si el nombre de tu archivo de clave pública SSH es diferente al del código de ejemplo, modifica el nombre del archivo para que coincida con tu configuración actual. Al copiar la clave, no añadas saltos de línea ni espacios en blanco.

```
$ cat ~/.ssh/id_ed25519.pub
```
2. En la esquina superior derecha de cualquier página de GitHub, haz clic en tu foto de perfil y luego en **Configuración** .
3.  En la sección "Acceso" de la barra lateral, haga clic en **Claves SSH y GPG** .
4. Haz clic en **Nueva clave SSH** o **Agregar clave SSH** .
5. En el campo "Título", añade una etiqueta descriptiva para la nueva clave. Por ejemplo, si usas un ordenador portátil personal, podrías llamar a esta clave "Ordenador portátil personal"
6. Seleccione el tipo de clave: autenticación o firma. Para obtener más información sobre la firma de confirmación, consulte [Acerca de la verificación de la firma de confirmación](https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification) .
7. En el campo "Clave", pegue su clave pública.
8. Haz clic en **Agregar clave SSH** .
9. Si se le solicita, confirme el acceso a su cuenta en GitHub. Para obtener más información, consulte [el modo Sudo](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/sudo-mode) .
-- end ignor
# Probando la conexcion SSH
una ves confugurado probar la conexcion
1. abrir terminal
2. introdusca
```
ssh -T git@github.com
# Intentos de conexión SSH a GitHub
```
posiblemente veas esta advertencia
```shell
> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
> ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
> Are you sure you want to continue connecting (yes/no)?
```
