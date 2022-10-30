# MySQL Commands

### Install MySQL
sudo apt update</br>
sudo apt install mysql-server

### Configure MySQL
sudo mysql</br>
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';</br>
exit</br>
sudo mysql_secure_installation</br>

sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf</br>
Set bind_address = 0.0.0.0</br>
sudo systemctl restart mysql</br>

sudo ufw allow from remote_IP_address to any port 3306

### User Management
CREATE USER 'user'@'host' IDENTIFIED BY 'password';</br>
GRANT PRIVILEGE ON database.table TO 'username'@'host';<br>