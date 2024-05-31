# nginx Image als Basis
FROM nginx

# Setzen des Arbeitsverzeichnis im Container
WORKDIR /usr/share/nginx/html

# Kopieren der HTML-Datei von meinem lokalen Arbeitsverzeichnis in das Container-Verzeichnis
COPY index.html .

# Öffne den Port 80 für den Zugriff auf die Webanwendung
EXPOSE 80