onpremises env

# Step by Step

## 1 - MariaDB installation

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
````
exit
````
