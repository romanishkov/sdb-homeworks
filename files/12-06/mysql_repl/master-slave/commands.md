# MASTER

CREATE USER 'replication'@'%' IDENTIFIED WITH mysql_native_password BY 'slaverepl';

GRANT REPLICATION SLAVE ON *.* TO 'replication'@'%';

SHOW GRANTS FOR 'replication'@'%';

SHOW MASTER STATUS;

# SLAVE

CHANGE MASTER TO MASTER_HOST='mysql-master',
MASTER_USER='replication',
MASTER_PASSWORD='slaverepl',
MASTER_LOG_FILE='mysql-bin.000003',
MASTER_LOG_POS=674;

START SLAVE;

SHOW SLAVE STATUS\G