# 📘 Apache HTTP Server en Arch Linux

## VirtualHosts, HTTPS/SSL y Análisis Básico de Seguridad

---

# 🧠 Objetivo del laboratorio

Aprender cómo funciona un servidor web real utilizando:

- Linux
    
- Apache HTTP Server
    
- VirtualHosts
    
- HTTPS / SSL
    
- Logs
    
- Diagnóstico y análisis básico de seguridad
    

---

# 🌐 1. ¿Qué es Apache?

Apache HTTP Server es un servidor web que:

- Escucha peticiones HTTP/HTTPS
    
- Sirve páginas web
    
- Trabaja mediante puertos
    
- Puede alojar múltiples sitios web en una sola máquina
    

Apache funciona como un proceso escuchando conexiones en:

|Puerto|Servicio|
|---|---|
|80|HTTP|
|443|HTTPS|

---

# 🐧 2. Instalación de Apache en Arch Linux

## Instalar Apache

```bash
sudo pacman -S apache
```

---

# ⚙️ 3. Manejo del servicio

## Iniciar Apache

```bash
sudo systemctl start httpd
```

## Habilitar al iniciar el sistema

```bash
sudo systemctl enable httpd
```

## Ver estado

```bash
sudo systemctl status httpd
```

## Reiniciar servicio

```bash
sudo systemctl restart httpd
```

---

# 🔎 4. Verificar funcionamiento

Abrir en navegador:

```text
http://localhost
```

Si carga una página → Apache está funcionando correctamente.

---

# 📁 5. Estructura importante de Apache en Arch Linux

|Ruta|Función|
|---|---|
|`/etc/httpd/conf/httpd.conf`|Configuración principal|
|`/etc/httpd/conf/extra/httpd-vhosts.conf`|VirtualHosts|
|`/srv/http/`|Sitios web|
|`/var/log/httpd/`|Logs|
|`/etc/hosts`|Dominios locales|

---

# 🧠 6. ¿Qué es un VirtualHost?

Un VirtualHost permite alojar múltiples sitios web en un mismo servidor.

Ejemplo:

- `miweb.local`
    
- `miblog.local`
    
- `api.local`
    

Todo funcionando en una sola instancia de Apache.

---

# 🔧 7. Habilitar VirtualHosts

Editar:

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

Buscar:

```apache
#Include conf/extra/httpd-vhosts.conf
```

Descomentar:

```apache
Include conf/extra/httpd-vhosts.conf
```

---

# 🌍 8. Configuración de dominio local

Editar:

```bash
sudo nano /etc/hosts
```

Agregar:

```text
127.0.0.1 miblog.local
```

Esto permite que Linux resuelva el dominio localmente.

---

# 📂 9. Crear sitio web

## Crear carpeta del sitio

```bash
sudo mkdir -p /srv/http/miblog
```

## Crear archivo web

```bash
sudo nano /srv/http/miblog/index.html
```

Ejemplo:

```html
<h1>Mi Blog con Apache 🚀</h1>
<p>Servidor funcionando correctamente</p>
```

---

# 🏗️ 10. Configuración básica del VirtualHost

Editar:

```bash
sudo nano /etc/httpd/conf/extra/httpd-vhosts.conf
```

Agregar:

```apache
<VirtualHost *:80>
    ServerName miblog.local
    DocumentRoot "/srv/http/miblog"

    ErrorLog "/var/log/httpd/miblog-error.log"
    CustomLog "/var/log/httpd/miblog-access.log" common
</VirtualHost>
```

---

# 🔍 11. Explicación de la configuración

|Directiva|Función|
|---|---|
|`VirtualHost *:80`|Escucha conexiones HTTP|
|`ServerName`|Dominio del sitio|
|`DocumentRoot`|Carpeta de la web|
|`ErrorLog`|Registro de errores|
|`CustomLog`|Registro de accesos|

---

# ✅ 12. Verificar configuración Apache

```bash
sudo apachectl configtest
```

Resultado esperado:

```text
Syntax OK
```

---

# 🔄 13. Reiniciar Apache

```bash
sudo systemctl restart httpd
```

---

# 🌐 14. Acceder al sitio

Abrir:

```text
http://miblog.local
```

---

# 🔒 15. ¿Qué es HTTPS?

HTTPS es HTTP cifrado mediante SSL/TLS.

Permite:

- Cifrar tráfico
    
- Proteger datos
    
- Evitar espionaje en la red
    
- Verificar identidad del servidor
    

HTTPS trabaja en:

|Puerto|Servicio|
|---|---|
|443|HTTPS|

---

# 🧠 16. Conceptos importantes de SSL/TLS

|Concepto|Explicación|
|---|---|
|Certificado|Identidad pública del servidor|
|Clave privada|Llave secreta usada para cifrado|
|HTTPS|HTTP + cifrado|
|TLS|Protocolo moderno de cifrado|
|Certificado autofirmado|Certificado creado por uno mismo|

---

# ⚙️ 17. Activar módulos SSL en Apache

Editar:

```bash
sudo nano /etc/httpd/conf/httpd.conf
```

Agregar o verificar:

```apache
LoadModule ssl_module modules/mod_ssl.so
LoadModule socache_shmcb_module modules/mod_socache_shmcb.so

Include conf/extra/httpd-ssl.conf
```

⚠️ El orden importa.  
Los módulos deben cargarse antes del `Include`.

---

# ❌ Error encontrado durante la práctica

## Error:

```text
SSLSessionCache: 'shmcb' session cache not supported
```

## Causa:

Faltaba cargar el módulo:

```apache
mod_socache_shmcb.so
```

## Solución:

```apache
LoadModule socache_shmcb_module modules/mod_socache_shmcb.so
```

---

# 🔑 18. Crear certificado SSL autofirmado

## Comando

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout /etc/httpd/conf/server.key \
-out /etc/httpd/conf/server.crt
```

---

# 🧠 19. Explicación del comando OpenSSL

|Parte|Función|
|---|---|
|`openssl`|Herramienta de cifrado|
|`req`|Solicitud de certificado|
|`-x509`|Crear certificado autofirmado|
|`-nodes`|No pedir contraseña|
|`-days 365`|Duración del certificado|
|`rsa:2048`|Tipo y tamaño de clave|
|`server.key`|Clave privada|
|`server.crt`|Certificado público|

---

# ⚠️ 20. Common Name (CN)

Durante la creación del certificado:

```text
Common Name (CN)
```

Debe coincidir con el dominio:

```text
miblog.local
```

---

# 🧠 21. Relación dominio y certificado

El certificado “dice”:

```text
Yo soy miblog.local
```

Si el navegador entra usando otro nombre:

⚠️ aparece advertencia de seguridad.

---

# 🔒 22. Configuración HTTPS del VirtualHost

Editar:

```bash
sudo nano /etc/httpd/conf/extra/httpd-vhosts.conf
```

Agregar:

```apache
# Redirección HTTP → HTTPS
<VirtualHost *:80>
    ServerName miblog.local
    Redirect "/" "https://miblog.local/"
</VirtualHost>

# HTTPS
<VirtualHost *:443>
    ServerName miblog.local
    DocumentRoot "/srv/http/miblog"

    SSLEngine on
    SSLCertificateFile "/etc/httpd/conf/server.crt"
    SSLCertificateKeyFile "/etc/httpd/conf/server.key"

    ErrorLog "/var/log/httpd/blog-ssl-error.log"
    CustomLog "/var/log/httpd/blog-ssl-access.log" common
</VirtualHost>
```

---

# 🔁 23. Verificar configuración nuevamente

```bash
sudo apachectl configtest
```

---

# 🔄 24. Reiniciar Apache

```bash
sudo systemctl restart httpd
```

---

# 🌍 25. Acceder usando HTTPS

```text
https://miblog.local
```

---

# ⚠️ 26. ¿Por qué aparece “No seguro”?

Porque el certificado es:

```text
autofirmado
```

El navegador:

- sí cifra la conexión
    
- pero no confía automáticamente en el certificado
    

---

# 🧠 27. Diferencia importante

|Tipo|Cifrado|Confianza|
|---|---|---|
|HTTP|❌|❌|
|HTTPS autofirmado|✅|❌|
|HTTPS con CA real|✅|✅|

---

# 🛡️ 28. Logs y análisis básico de seguridad

## Ver accesos en tiempo real

```bash
tail -f /var/log/httpd/access.log
```

Permite ver:

- IP
    
- navegador
    
- rutas solicitadas
    
- códigos HTTP
    

---

# ⚠️ 29. Ver errores

```bash
tail -f /var/log/httpd/error.log
```

---

# 💀 30. Simular accesos sospechosos

```bash
curl -k https://miblog.local/admin
```

O:

```bash
curl -k https://miblog.local/phpmyadmin
```

Esto genera registros similares a bots reales buscando vulnerabilidades.

---

# 🔍 31. Buscar errores 404

```bash
grep "404" /var/log/httpd/miblog-ssl-access.log
```

Permite detectar:

- rutas inexistentes
    
- escaneos automáticos
    
- bots
    

---

# 🌐 32. Escaneo básico con Nmap

```bash
nmap -sV miblog.local
```

Permite detectar:

- puertos abiertos
    
- servicios
    
- versiones
    

---

# 📡 33. Análisis de tráfico de red

## Ver tráfico HTTPS

```bash
sudo tcpdump -i any port 443
```

Con HTTPS:

- el tráfico viaja cifrado
    
- no puede leerse fácilmente
    

---

# 🧠 34. Diferencia entre HTTP y HTTPS

|HTTP|HTTPS|
|---|---|
|texto plano|cifrado|
|visible|protegido|
|inseguro|seguro|

---

# 🎯 35. Lo aprendido realmente

## Administración

- Linux
    
- Apache
    
- VirtualHosts
    
- HTTPS
    
- SSL/TLS
    
- Logs
    
- Configuración de servicios
    
- Troubleshooting
    

## Seguridad básica

- Certificados
    
- Cifrado
    
- Logs
    
- Detección de rutas sospechosas
    
- Escaneo básico
    
- Inspección de tráfico
    

---

# 🚀 36. Próxima etapa: NGINX

Siguientes temas:

- Arquitectura moderna
    
- Reverse Proxy
    
- Proxy Pass
    
- Balanceo de carga
    
- Rendimiento
    
- Integración con aplicaciones reales
    
- Hardening
    

🔥 NGINX es muy usado en servidores modernos y cloud.
