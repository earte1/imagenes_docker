# Usa la imagen oficial de WordPress como base
FROM wordpress:6.6.2-php8.3

# Define una variable de entorno para el tamaño máximo de archivo (en MB)
ENV PHP_UPLOAD_MAX_FILESIZE 128M
ENV PHP_UPLOAD_MAX_FILESIZE 128M

# Copia el archivo de configuración de PHP personalizado
COPY uploads.ini /usr/local/etc/php/conf.d/
COPY apache2.conf /etc/apache2/conf-available/custom-timeout.conf

# Habilitar los módulos proxy y proxy_http de Apache
RUN a2enmod proxy
RUN a2enmod proxy_http
RUN a2enconf custom-timeout

# Reiniciar Apache para aplicar los cambios
RUN service apache2 restart

