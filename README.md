# LAMP construido con Docker Compose

Este es un entorno de LAMP básico creado con Docker Compose. Se instalan los siguientes programas:

* PHP 7.1
* Apache 2.4
* MySQL 5.7
* phpMyAdmin

## Instalación

Clone este repositorio y cambie a la rama `7.1.x`. Ejecuta `docker-compose up -d`.

```shell
git clone git@github.com:televisa-digital/apps-feeds-generator.git docker-compose-lamp
cd docker-compose-lamp/
git fetch --all
git checkout 7.1.x
cp sample.env .env
docker-compose up -d
```

LAMP ya está listo!! Puedes acceder a través de `http://localhost`.

## Configuración

Este paquete viene con opciones de configuración predeterminadas. Puede modificarlos creando el archivo `.env` en su directorio raíz.

Para hacerlo más fácil, simplemente copie el contenido del archivo `sample.env` y actualice los valores de las variables de entorno según sus necesidades.

### Configuración de variables


Existen las siguientes variables de configuración disponibles y puedes personalizarlas sobrescribiéndolas en su propio archivo `.env`.

_**DOCUMENT_ROOT**_

Es un documento raíz para el servidor Apache. El valor predeterminado para esto es `. /www`. Todos sus sitios irán aquí y se sincronizarán automáticamente.

_**MYSQL_DATA_DIR**_

Este es el directorio de datos MySQL. El valor predeterminado para esto es `. /data/mysql`. Todos sus archivos de datos MySQL se almacenarán aquí.

_**VHOSTS_DIR**_

Esto es para hosts virtuales. El valor predeterminado para esto es `. /config/vhosts`. Puede colocar sus archivos conf de hosts virtuales aquí.

> Asegúrese de agregar una entrada al archivo `hosts` de su sistema para cada host virtual.

_**APACHE_LOG_DIR**_

Esto se usará para almacenar registros de Apache. El valor predeterminado para esto es `./logs/apache2`.

_**MYSQL_LOG_DIR**_

Esto se usará para almacenar registros de Apache. El valor predeterminado para esto es `./logs/mysql`.


## Servidor Web

Apache está configurado para ejecutarse en el puerto 80. Por lo tanto, puede acceder a través de `http://localhost`.

#### Modulos Apache

Por defecto, los siguientes módulos están habilitados.

* Rewrite
* Headers

> Si deseas habilitar más módulos, simplemente actualice `./bin/webserver/Dockerfile`.
> Tienes que reconstruir la imagen ejecutando`docker-compose build` y reiniciar los contenedores.

#### Conexión vía SSH

Puede conectarse al servidor web utilizando `docker-compose exec` comando para realizar varias operaciones en él. Utilice el siguiente comando para iniciar sesión en el contenedor a través de ssh.

```shell
docker-compose exec webserver bash
```

## PHP

La versión instalada de PHP es 7.1.

#### Extensiones

Por defecto se instalan las siguientes extensiones.

* mysqli
* mbstring
* zip
* intl
* mcrypt
* curl
* json
* iconv
* xml
* xmlrpc
* gd

> Si deseas instalar más extensiones, solo actualice `./bin/webserver/Dockerfile`.
> Tienes que reconstruir la imagen ejecutando `docker-compose build` y reiniciar los contenedores de Docker.

## phpMyAdmin

phpMyAdmin está configurado para ejecutarse en el puerto 8080. Use las credenciales predeterminadas.

http://localhost:8080/  
username: root  
password: tiger

## Cron
Para poder configurar las tareas programadas hay que realizar los siguientes:

    1.-Crear un archivo en el directorio /bin/cron/nombre_archivo.sh y agregar el curl a la petición ( ver el archivo test.sh ).
    2.-Modificar el archivo /bin/cron/entrypoint.sh. Para agregar las configuraciones del crontab.