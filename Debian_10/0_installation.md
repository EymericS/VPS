# FIRST THINGS TO INITIATE THE VPS

## First connection on SSH :
* change unix user password : `~$ passwd`
* get update : `~$ sudo apt-get update`
* apply update : `~$ sudo apt-get upgrade`

## HTTP server install :
* install apache2 `~$ sudo apt-get install apache2`
> Test apache2 install: http://xxx.xxx.xxx.xxx/ (IP)
* delete redirection on apache2 default home page : delete line #RedirectMatch ^/$ /apache2-default/ in /etc/apache2/sites-available/default

## PHP language :
* `~$ sudo apt-get install php`
* *php dependencies* : `~$ sudo apt-get install php-curl php-gd php-bz2 php-zip php-json php-mbstring php-xml`

## MySQL DataBase ( *MariaDB* ) :
* `~$ sudo apt install mariadb-server`
* login : `~$ sudo mysql`
* list DB users : `~> SELECT user, host, plugin, password FROM mysql.user;`
* New user :
````
~> CREATE USER 'username'@'localhost' IDENTIFIED BY 'mpassword';
  or
~> CREATE USER 'unix_username'@'localhost' IDENTIFIED WITH unix_socket;
````
* using of mysql by php : `~$ sudo apt install php-mysql`

## PhpMyAdmin :
* Dep : `~$ sudo aptitude -t buster-backports install php-twig`
* install : `~$ sudo apt-get install phpmyadmin`
* Apache include : `~$ sudo vim /etc/apache2/apache2.conf` /* add `Include /etc/phpmyadmin/apache.conf` at the end
* Create PMA User : `~$ sudo mysql`
````sql
  CREATE USER 'pma_username'@'localhost' IDENTIFIED BY 'pma_pwd';
  GRANT ALL ON *.* TO 'pma_username'@'localhost' WITH GRANT OPTION;
  FLUSH PRIVILEGES;
  QUIT;
````
>Try http://xxx.xxx.xxx.xxx/phpmyadmin to test install

## DNS server :
* `~$ sudo apt-get install bind9`

## Mail server :
`~$ sudo apt-get install postfix postfix-mysql` no config choice

## TODO List :
- [x] Change pwd
- [x] Install HTTP **(apache2)**
- [ ] Delete /apache2-default/ redirection
- [x] Install PHP
- [x] Install DataBase **(MariaDB)**
- [x] Install DNS server
- [x] Install Mail server
