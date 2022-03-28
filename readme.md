## Docker con WP + PHP + Apache + WP-CLI + Mysql + PMA + SSL


### Instalación / configuración

- La plantilla está configurada para crear certificados SSL a través de mkcert, para poder tener nuestro dominio bajo SSL, intrucciones para instalarlo: https://github.com/FiloSottile/mkcert
- Se puede elegir la versión de WordPress y de PHP cambiando la primera sentencia del `Dockerfile` eligiendo cualquiera de las imágenes oficiales disponibles en https://hub.docker.com/_/wordpress/
- El resto de contenedores/servicios están indicados desde el archivo `docker-compose.yml`
- Xdebug queda instalado en el servicio `wp` que es el que contiene WordPress, PHP y Apache.
- Modificar las variables de entorno del archivo `.env` por las de nuestro proyecto particular.
- Modificar archivo `000-default.conf`, indicando el nombre correcto de los certificados que hayamos creado previamente



#### Archivos personalizados

- `.htaccess`
- `000-default.conf`
- `php.conf.ini`
- `xdebug.ini`



### Puesta en marcha

1. ```git clone git@github.com:josandreu/docker-wp-php-apache.git```
2. ```cd docker/config/```
3. ```mkdir ssl && cd ssl```
4. `mkcert -install nombre-dominio-proyecto`
5. Modificamos el archivo `000-default.conf`, indicando el nombre correcto de SSLCertificateFile y SSLCertificateKeyFile, que corresponderán a los nombres de los certificados que hayamos creado previamente con mkcert.
6. `cd ../../..`
7. `docker-compose up -d`


### WP-CLI

Para ejecutar wp-cli: `docker-compose run --rm wpcli {comando}`

Nos muestra la info del contenedor de wp-cli: `docker-compose run --rm wpcli`

Para mostrar los usuarios de WP: `docker-compose run --rm wpcli user list`



