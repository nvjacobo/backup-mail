## Respaldo de correo con Getmail

Getmail es un “mail retriever” diseñado para descargar correo electrónico de uno o más buzones de correo a través de servidores o máquinas locales. Mantenido por Charles Cazabon y publicado bajo licencia GPL.

A continuación describimos cómo utilizar Getmail en Debian Buster para realizar un respaldo de un buzón de correo electrónico, en un servidor remoto, a nuestra máquina local. 

Getmail tiene soporte para los siguientes protocolos para acceder a buzones de correo electrónico. 

* POP3
* POP3 sobre SSL
* IMAP4 sobre SSL

### Instalación 

Getmail está disponible para varios de los gestores de paquetería de sistemas operativos GNU/Linux. Para este caso vamos a proceder a instalarlo en Debian 10. 

#sudo apt install getmail 

### Configuración y uso 

Crear un directorio de configuración y establecimiento de permisos: 

```
$ mkdir -m 0700 ~/.getmail
```

Creamos el archivo de configuración

```
$touch ~/.getmail/getmailrc
```

Creamos el directorio en donde vamos a realizar el respaldo. En este caso lo vamos a generar dentro del home del usuario.

```
$mkdir ~/respaldo
```
Con getmail es posible descargar tanto mbox y maildir. Para este caso vamos a utilizar maildar. Por lo que es necesario crear dentro de nuestro directorio destino de respaldos cur, new y tmp.

```
$ cd respaldo
```
```
$mkdir cur new tmp
```

Ahora vamos a editar nuestro archivo de configuración. Para indicar el servidor y usuario, con el editor de nuestra elección.

```
$vim ~/.getmail/getmailrc
```

#### Configuración

Agregamos las siguientes lineas a getmailrc

```
[retriever]
type = SimpleIMAPSSLRetriever
server = servidor.net
username = USER
password = PASS 
[destination] 
type = Maildir 
path = ~/respaldo/
# lineas adicionales para no alterar el estado del buzón en el servidor
delivered_to = false
received = false
```

Adicionalmente agregamos la siguiente variable para evitar que se descargue todo el correo del servidor cada vez que se ejecute getmail y así solo descargué el correo no descargado previamente. 

```
[options]
read_all = False

```

Por default Getmail descarga la carpeta INBOX. Si desea descargar todas las carpetas de su buzón tendrá que utilizar la siguiente variable, para su archivo de configuración. 

```
mailboxes = ALL

```




Finalmente corremos getmail

```
$getmail
```

### Referencias 


Getmail documentation http://pyropus.ca/software/getmail/documentation.html










































