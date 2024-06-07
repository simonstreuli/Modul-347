### Schritt 1: Dockerfile für die Datenbank (DB) erstellt
 
Das Dockerfile für die Datenbank bleibt unverändert. Du definierst weiterhin das Basis-Image, setzt die Umgebungsvariablen und legst den Port fest:
 
```Dockerfile
# Basis-Image
FROM mariadb
 
# Umgebungsvariablen setzen
ENV MYSQL_ROOT_PASSWORD=noris
ENV MYSQL_DATABASE=mysql
ENV MYSQL_USER=admin
ENV MYSQL_PASSWORD=myuserpassword
 
EXPOSE 3306
```
 
### Schritt 2: Docker-Build für die Datenbank durchgeführt
 
Führe den Docker-Build-Befehl aus, um das Image für die Datenbank zu erstellen:
 
```bash
docker build -f Dockerfile -t kn02b-db .
```
 
### Schritt 3: Docker-Run für die Datenbank
 
Starte den Datenbank-Container ohne die Verbindung zu einem spezifischen Netzwerk:
 
```bash
docker run --name kn02b-db -d -p 3307:3306 kn02b-db
```
 
### Schritt 4: Dockerfile für die Webseite (Web) erstellt
 
Das Dockerfile für die Webseite bleibt gleich. Du kopierst die Dateien, installierst PHP mysqli und definierst den Port:
 
```Dockerfile
# Dockerfile für die Webseite
 
# Basis-Image
FROM php:8.0-apache
 
# Dateien kopieren
COPY info.php /var/www/html/
COPY db.php /var/www/html/
 
# PHP mysqli installieren
RUN docker-php-ext-install mysqli
 
EXPOSE 80
```
 
### Schritt 5: Docker-Build für die Webseite durchgeführt
 
Erstelle das Image für die Webseite mit dem gleichen Befehl:
 
```bash
docker build -f DockerfileWeb -t kn02b-web .
```
 
### Schritt 6: Docker-Run für die Webseite mit --link
 
Starte den Web-Container und verwende `--link` um eine Verbindung zur Datenbank herzustellen. Dies ermöglicht der Webseite, auf die Datenbank zuzugreifen:
 
```bash
docker run --name kn02b-web --link kn02b-db:mysql -d -p 8080:80 kn02b-web
```
 
Mit `--link kn02b-db:mysql` wird der Datenbank-Container (kn02b-db) im Web-Container unter dem Alias `mysql` verfügbar gemacht. Das ermöglicht es deiner Webanwendung, über `mysql` auf die Datenbank zuzugreifen.
 
### Überprüfung
 
Die Überprüfung bleibt gleich. Du kannst durch Zugriff auf die Webseiten info.php und db.php im Browser sicherstellen, dass die Verbindung funktioniert. Beachte jedoch, dass `--link` eine veraltete Funktion ist und Docker Netzwerke für neue Implementierungen empfiehlt.
 
### Schritt 8: Überprüfung durchgeführt
 
Um sicherzustellen, dass die Kommunikation funktioniert, habe ich einen Telnet-Befehl für den Zugriff auf den DB-Server durchgeführt und Screenshots der Seiten info.php und db.php gemacht, um ihre Funktionalität zu überprüfen.
 