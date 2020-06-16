> First connection on SSH :
# passwd /* change unix user password */
# sudo apt-get update
# sudo apt-get upgrade

> Serveur HTTP :
# sudo apt-get install apache2
/* Test apache install: http://xxx.xxx.xxx.xxx/ (IP) */

> TODO ? 
#RedirectMatch ^/$ /apache2-default/

> PHP language :
# sudo apt-get install php
# sudo apt-get install php-curl php-gd php-bz2 php-zip php-json php-mbstring php-xml
/* php dependencies */

> MySQL DataBase ( MariaDB ) :
# sudo apt install mariadb-server
# sudo mysql /* login */
# SELECT user, host, plugin, password FROM mysql.user; /* list DB users */
  > New user : 
  # CREATE USER 'username'@'localhost' IDENTIFIED BY 'mpassword';
  or
  # CREATE USER 'unix_username'@'localhost' IDENTIFIED WITH unix_socket;
# sudo apt install php-mysql /* using of mysql by php */

> PhpMyAdmin :
  > Dep :
  # sudo aptitude -t buster-backports install php-twig
# sudo apt-get install phpmyadmin
/* root user pwd & apache config */
  > Apache include
  # sudo vim /etc/apache2/apache2.conf /* add "Include /etc/phpmyadmin/apache.conf" at the end"
  > Create PMA User :
  # sudo mysql
  # CREATE USER 'pma_username'@'localhost' IDENTIFIED BY 'pma_pwd';
  # GRANT ALL ON *.* TO 'pma_username'@'localhost' WITH GRANT OPTION;
  # FLUSH PRIVILEGES;
  # QUIT;
/* Try http://xxx.xxx.xxx.xxx/phpmyadmin to test install */

> DNS server :
# sudo apt-get install bind9

> Mail server :
# sudo apt-get install postfix postfix-mysql
/* no config choice */
