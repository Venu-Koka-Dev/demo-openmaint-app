# Update System
sudo apt-get update -y
sudo apt-get upgrade
sudo apt install unzip

# Install Java
sudo apt-get install openjdk-17-jdk
java -version

# Install Postgres
wget —quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - 
echo "deb http://apt.postgresql.org/pub/repos/apt/  $(lsb_release -cs)-pgdg main" | sudo tee /etc/apt/sources.list.d/postgresql-pgdg.list &gt;  /dev/null
sudo apt-get update
sudo apt-get install postgresql-12
sudo apt install postgresql-12-postgis-3 libpostgis-java
sudo passwd postgres
## Password: postgrespass
sudo usermod -aG sudo postgres
sudo -u postgres psql template1
ALTER USER postgres WITH PASSWORD 'admin123';
## To exit from the Postgres prompt: \q
## Password: admin123

wget http://dl.alfresco.com/release/community/build-3370/alfresco-community-3.4.d-installer-linux-x64.bin
chmod a+x alfresco-community-3.4.d-installer-linux-x64.bin
sudo ./alfresco-community-3.4.d-installer-linux-x64.bin --mode text

Choose 'English' (Type in 1)
﻿﻿Accept: SharePoint, Records Management, Web Quick Start, Web Project management
﻿﻿Select an Installation Type: 1 - Easy
﻿Leave the installation folder as default
﻿﻿Select the bundled MySQL database: Type in 1
﻿﻿Create the database password (Just type them in)
﻿﻿Create Alfresco's password (Just type them in)
﻿﻿Decline the installation as a service (It breaks anyways, so we're handling it ourselves. (type n)
View Readme file- n

cd  /opt/alfresco-3.4.d 
sudo ./alfresco.sh status

# Jika status RUNNING
sudo ./alfresco.sh stop

# Update the Tomcat file - server.xml
sudo nano tomcat/conf/server.xml
// In Line 22: ‹Server port="8006" shutdown="SHUTDOWN">
// In Line 69: (lol) «Connector port="8081" URIEncoding="UTF-8" protocol="НТТР/1.1" connectionTimeout="20000" redirectPort="8443" />

sudo ./alfresco.sh start

# Install GeoServer
sudo adduser geoserver;sudo usermod -aG sudo geoserver;sudo su - geoserver 
## Password: geoserver123
wget https://sourceforge.net/projects/geoserver/files/GeoServer/2.21.0/geoserver-2.21.0-t
unzip -d /home/geoserver/server geoserver-2.21.0-bin.zip 
nano /home/geoserver/server/start.ini

Ubah port jetty.http.port menjadi jetty.http.port=8082
Buat file service geoserver agar bisa berjalan otomatis $ sudo nano /usr/lib/systemd/system/geoserver.service

[Unit]

Description=GeoServer Service

After=network. target
