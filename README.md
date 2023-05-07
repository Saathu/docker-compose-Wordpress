# LB2

## Inhaltsverzeichnis
- [Einleitung](#einleitung)
- [Service-Beschreibung](#service-beschreibung)
- [Umsetzung](#umsetzung)
- [Anwendung](#anwendung)
- [Quellen](#quellen)
- [Tools](#tools)

## Einleitung
Im Rahmen meines Projekts habe ich ein Docker Compose File erstellt, das einen Wordpress-Container und einen Datenbank-Container erstellt. Docker ist eine Software-Plattform, die es ermöglicht, Anwendungen in sogenannten Containern zu isolieren und auszuführen. Dadurch wird es einfacher, Anwendungen auf unterschiedlichen Systemen auszuführen, da alle notwendigen Abhängigkeiten innerhalb des Containers enthalten sind.

## Service-Beschreibung
Mein Docker Compose File erstellt zwei Docker-Container, einen für Wordpress und einen für MySQL-Datenbank. Der Wordpress-Container enthält die Wordpress-Software, die es dem Benutzer ermöglicht, eine Website zu erstellen und zu hosten, während der MySQL-Container die notwendige Datenbank für Wordpress bereitstellt.

Der Datenbank-Container ist so konfiguriert, dass er die MySQL-Datenbank verwendet, die von Wordpress benötigt wird, um Daten zu speichern. Dabei werden alle Datenbank-Verbindungsparameter in der Umgebungsvariable definiert.

Beide Container sind so konfiguriert, dass sie automatisch beim Starten des Docker Compose Files erstellt und gestartet werden. Dabei wird der Wordpress-Container auf Port 80 und der Datenbank-Container auf Port 3306 ausgeführt.

Die Verwendung des Docker Compose Files ermöglicht es Benutzern, schnell und einfach eine Wordpress-Website und eine MySQL-Datenbank zu erstellen und zu hosten, ohne dass sie sich um die Installation und Konfiguration der Software kümmern müssen.

## Umsetzung
Zuerst habe ich eine Ubunut VM in VMware erstellt und anschliessend git, docker und docker-compose installiert.

git install
```
sudo apt install git
```
docker install
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add 
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt update
sudo apt install docker-ce
```
docker-compose install
```
sudo apt install docker-compose 
```

Danach habe ich das Docker Compose File geschrieben. Dabei habe ich alle erforderlichen Konfigurationen eingegeben, um sicherzustellen, dass der Wordpress-Container und der Datenbank-Container richtig erstellt werden. 

```
version: '3'
services:
  db:
    #Neuste Version mysql Image
    image: mysql:latest
    #wegen Error
    command: '--default-authentication-plugin=mysql_native_password'
    #startet Container neu, falls aus wegen error
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=somewordpress
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=Testuser
      - MYSQL_PASSWORD=wordpress
    # exposed Container port mysql
    expose:
      - 3306
  wordpress:
    image: wordpress:latest
    # host port mit Container port verbinden
    ports:
      - 80:80
    restart: always
    environment:
      - WORDPRESS_DB_HOST=db
      - WORDPRESS_DB_USER=Testuser
      - WORDPRESS_DB_PASSWORD=wordpress
      - WORDPRESS_DB_NAME=wordpress
```
Schritt 4: Docker Compose File ausführen
Als nächstes habe ich das Docker Compose File ausgeführt, um die beiden Container zu erstellen und zu starten. Ich habe dabei den Befehl "docker-compose up" in der Terminal-Shell ausgeführt, um den Prozess zu starten.
![image](https://user-images.githubusercontent.com/101107564/236688298-ec539fae-babc-4671-b9ed-d5b4e3a7d2fc.png)

Schritt 5: Website testen
Nachdem die Container erstellt und gestartet wurden, habe ich die Wordpress-Website getestet, indem ich meinen Webbrowser geöffnet und http://localhost aufgerufen habe. Hier konnte ich dann die Standard-Wordpress-Seite sehen.
![image](https://user-images.githubusercontent.com/101107564/236688433-81b2c646-50cd-485b-a2ee-1cfd076b3dd8.png)

## Anwendung 

Öffnen Sie das Terminal oder die Befehlszeile auf Ihrem Computer und navigieren Sie zu dem Ordner, in dem Sie das Docker Compose File speichern möchten. Führen Sie dann den folgenden Befehl aus, um das Repository zu klonen:
```
git clone https://github.com/Saathu/docker-compose-Wordpress.git
```

Navigieren Sie nun in den Ordner, in dem das Docker Compose File gespeichert ist.
````
cd docker-compose-Wordpress
````
Führen Sie den folgenden Befehl aus, um das Docker Compose File auszuführen:
````
sudo docker-compose up
````
oder folgenden Befehl ausführen um im hintergrund laufen zu lassen:
````
sudo docker-compose up -d
````
Sobald die Container erstellt und gestartet wurden, können Sie die Wordpress-Website testen, indem Sie Ihren Webbrowser öffnen und http://localhost aufrufen. Hier sollten Sie dann die Standard-Wordpress-Seite sehen können.

## Quellen
https://support.netfoundry.io/hc/en-us/articles/360057865692-Installing-Docker-and-docker-compose-for-Ubuntu-20-04
https://docs.docker.com/samples/wordpress/

## Tools
Docker
