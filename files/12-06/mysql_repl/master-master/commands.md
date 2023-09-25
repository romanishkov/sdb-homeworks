# MASTER-1

CREATE USER 'replication'@'%' IDENTIFIED WITH mysql_native_password BY 'pass';

GRANT REPLICATION SLAVE ON *.* TO 'replication'@'%';

SHOW GRANTS FOR 'replication'@'%';

SHOW MASTER STATUS;

CHANGE MASTER TO MASTER_HOST='mysql-master-2',
MASTER_USER='replication',
MASTER_PASSWORD='pass',
MASTER_LOG_FILE='mysql-bin.000003',
MASTER_LOG_POS=674;

# MASTER-2

CREATE USER 'replication'@'%' IDENTIFIED WITH mysql_native_password BY 'pass';

GRANT REPLICATION SLAVE ON *.* TO 'replication'@'%';

SHOW GRANTS FOR 'replication'@'%';

SHOW MASTER STATUS;

CHANGE MASTER TO MASTER_HOST='mysql-master-1',
MASTER_USER='replication',
MASTER_PASSWORD='pass',
MASTER_LOG_FILE='mysql-bin.000003',
MASTER_LOG_POS=674;

START SLAVE;

SHOW SLAVE STATUS\G