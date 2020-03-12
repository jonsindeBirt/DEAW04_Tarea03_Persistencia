# Creamos la imagen a partir de Ubuntu 18.04
FROM ubuntu:18.04

# Instalamos apache y el módulo que permite conectar con php. Lo habilitamos.
# Clonamos el repositorio github y lo copiamos a /var/www/html/
RUN apt-get update && apt-get install -y apache2 \
    && apt-get -y install libapache2-mod-fcgid \
    && a2enmod proxy_fcgi \
    && apt-get install -y git \
    && git clone https://github.com/deaw-birt/despliegue-PHP.git \
    && cp /despliegue-PHP/php/*.* /var/www/html/ \
    && rm -R /despliegue-PHP/

# Cargamos la configuración del servidor y el proyecto web.
COPY 000-default.conf /etc/apache2/sites-available
# COPY index.php dwes.css /var/www/html/

EXPOSE 80

# Arrancamos el servidor apache una vez que se ha creado el contenedor
# Así no hay que acceder a él para ponerlo en marcha
CMD ["apachectl", "-D", "FOREGROUND"]