# MySQL Commands

## Install MySQL
sudo apt update</br>
sudo apt install mysql-server

## Configure MySQL
sudo mysql</br>
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';</br>
exit</br>
sudo mysql_secure_installation</br>

sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf</br>
Set bind_address = 0.0.0.0</br>
sudo systemctl restart mysql</br>

sudo ufw allow from remote_IP_address to any port 3306

## User Management
CREATE USER 'user'@'host' IDENTIFIED BY 'password';</br>
GRANT PRIVILEGE ON database.table TO 'username'@'host';<br>
DROP USER 'user'@'host';</br>

## Replication
### On Master
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf</br>
log-bin=mysql-bin</br>
server-id=1</br>

### On Slave
server-id=2</br>

### Create user on Master
mysql> CREATE USER 'repl'@'%.example.com' IDENTIFIED BY 'password';</br>
mysql> GRANT REPLICATION SLAVE ON *.* TO 'repl'@'%.example.com';</br>

### Make Backup
xtrabackup --backup --target-dir=/path/to/mysql/backupdir --user=user --password=password</br>
xtrabackup --prepare --target-dir=/path/to/mysql/backupdir --user=user --password=password</br>

### Transfer Backup
rsync -avpPzO --no-owner --no-group --no-perms  -e ssh /path/to/mysql-backup/ user@host:/path/to/mysql-backup</br>

### Restore Backup
xtrabackup --move-back --target-dir=/path/to/mysql/backupdir</br>
chown -R mysql:mysql /path/to/mysql/datadir/*</br>

## Installing Percona Tools
### XtraBackup
wget https://repo.percona.com/apt/percona-release_latest.$(lsb_release -sc))\_all.deb</br>
sudo dpkg -i percona-release_latest.$(lsb_release -sc)\_all.deb</br>
sudo percona-release enable-only tools release</br>
sudo apt update</br>
sudo apt install percona-xtrabackup-24</br>
sudo apt install qpress</br>
### Percona Toolkit
sudo percona-release setup pt</br>
sudo apt-get install percona-toolkit</br>
