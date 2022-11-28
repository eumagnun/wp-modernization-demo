onpremises env

# Step by Step

## 1 - MariaDB installation on database-wp VM

````
sudo apt update
````
````
sudo apt install mariadb-server
````
````
sudo systemctl start mariadb.service
````
````
sudo mysql_secure_installation
````
````
sudo mariadb
````
````
GRANT ALL ON *.* TO 'admin'@'localhost' IDENTIFIED BY 'demo123' WITH GRANT OPTION;
````
````
FLUSH PRIVILEGES;
````

*create user (replace IP by your server IP)
````
sudo mysql -u root -p
CREATE DATABASE wordpress;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'wpuser';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
CREATE USER 'wpuser'@'10.0.0.3' IDENTIFIED BY 'wpuser';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'10.0.0.3';
FLUSH PRIVILEGES;
exit
````
````
exit
````

## 2 - Wordpress installation on app-wp VM
````
sudo apt update
````
````
sudo apt update
sudo apt install apache2 \
                 ghostscript \
                 libapache2-mod-php \
                 php \
                 php-bcmath \
                 php-curl \
                 php-imagick \
                 php-intl \
                 php-json \
                 php-mbstring \
                 php-mysql \
                 php-xml \
                 php-zip
````
````
sudo wget https://wordpress.org/latest.tar.gz
````
````
sudo tar zx -f latest.tar.gz -C /srv/www
````
````
sudo nano /etc/apache2/sites-available/wordpress.conf
````
* Add the content bellow:
````
<VirtualHost *:80>
    DocumentRoot /srv/www/wordpress
    <Directory /srv/www/wordpress>
        Options FollowSymLinks
        AllowOverride Limit Options FileInfo
        DirectoryIndex index.php
        Require all granted
    </Directory>
    <Directory /srv/www/wordpress/wp-content>
        Options FollowSymLinks
        Require all granted
    </Directory>
</VirtualHost>
````
* enable the new site
````
sudo a2ensite wordpress
````
* enable URL rewriting
````
sudo a2enmod rewrite
````
*  disable the dedafult site and restart the service
````
sudo a2dissite 000-default
sudo service apache2 restart
sudo service apache2 reload
````


## Util
* list services and ports
````
netstat -tln
````
