# My-First-Docker

Practica docker: mi primer docker realizado con [@MatiasAGomezJ], [@Durutui] (Arturo) y [@JoanLlompart].

 #### Preparamos el directorio donde copiaremos los archivos locales al contenedor, para ello, utilizaremos el comando:

  ![](https://media.discordapp.net/attachments/944739503904526388/945034358165766144/ls.png)

  Para el DockerFile:
  ```sql
  # heredamos la imagen de DEBIAN
  FROM DEBIAN

  # establecemos la zona horaria
  ENV TZ=Europe/Madrid

  # instalamos php 7.3 y apache
  # incluimos procps y telnet para que pueda usarlos con el indicador shell.sh
  RUN apt-get update -qq >/dev/null && apt-get install -y -qq procps telnet apache2 php7.4 -qq >/dev/null

  # HTML server directorio
  WORKDIR /var/www/html
  COPY . /var/www/html/

  # La aplicación PHP guardará su estado en /data, por lo que creamos /data dentro del contenedor
  RUN mkdir /data && chown -R www-data /data && chmod 755 /data & chmod 775 -R /var/www/html/

  # Necesitamos un archivo de configuración php personalizado para habilitar los directorios de usuario
  COPY php.conf /etc/apache2/mods-available/php7.3.conf

# Habilitar directorio de usuario y php
RUN a2enmod php7.4

# ejecutamos un script para iniciar el servidor; la sintaxis de la matriz hace que ^C funcione como queremos
CMD  ["./entrypoint.sh"]
  ```

Ahora, procederemos a lanzar el script con `Build sh`
![](https://media.discordapp.net/attachments/944739503904526388/945034358341898250/build.png?width=1620&height=502)

Y para finalizar, lanzaremos el contenedor con `debug.sh`, para comprobar que funciona correctamente
![](https://media.discordapp.net/attachments/944739503904526388/945035128655200356/debug.png?width=1620&height=702)
