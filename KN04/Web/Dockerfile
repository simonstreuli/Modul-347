# Verwenden Sie das offizielle PHP-Image mit Apache als Basis
FROM php:8.0-apache

# Kopieren Sie die PHP-Dateien in das Arbeitsverzeichnis des Containers
COPY info.php /var/www/html/
COPY db.php /var/www/html/

# Installieren Sie das PHP mysqli-Modul
RUN docker-php-ext-install mysqli

# Port für den Apache-Webserver öffnen
EXPOSE 80
