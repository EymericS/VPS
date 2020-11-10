# FIRST THINGS TO INITIATE THE VPS

## TODO List from WEB :
- [ ] Update the system
sudo apt update && sudo apt upgrade
- [ ] Enable additional repositories for more software
- [ ] Free space
sudo apt-get autoremove
sudo du -sh /var/cache/apt
- [ ] setup mail client ?
- [ ] Install Timeshift ?
- [ ] fail2ban ?
- [ ] iptables
- [ ] root user
change root password `sudo passwd root`
lock usr root `sudo passwd -l root`
change root pwd to unlock
- [ ] secure ssh
diasable ssh root login `vim /etc/ssh/sshd_config` `PermitRootLogin no` `/etc/init.d/ssh restart`
force not empty password 'vim /etc/ssh/sshd_config' 'PermitEmptyPasswords no'
chnage port 22
- [ ] firewall
setup a firwall `sudo ufw status` at end put `tmpfs     /dev/shm     tmpfs     defaults,noexec,nosuid     0     0`
- [ ] Secure shared memory
`sudo vi /etc/fstab` 
- [ ] network secur
`sudo vi /etc/sysctl.conf` put `
# IP Spoofing protection
net.ipv4.conf.all.rp_filter = 1
net.ipv4.conf.default.rp_filter = 1

# Ignore ICMP broadcast requests
net.ipv4.icmp_echo_ignore_broadcasts = 1

# Disable source packet routing
net.ipv4.conf.all.accept_source_route = 0
net.ipv6.conf.all.accept_source_route = 0 
net.ipv4.conf.default.accept_source_route = 0
net.ipv6.conf.default.accept_source_route = 0

# Ignore send redirects
net.ipv4.conf.all.send_redirects = 0
net.ipv4.conf.default.send_redirects = 0

# Block SYN attacks
net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_max_syn_backlog = 2048
net.ipv4.tcp_synack_retries = 2
net.ipv4.tcp_syn_retries = 5

# Log Martians
net.ipv4.conf.all.log_martians = 1
net.ipv4.icmp_ignore_bogus_error_responses = 1

# Ignore ICMP redirects
net.ipv4.conf.all.accept_redirects = 0
net.ipv6.conf.all.accept_redirects = 0
net.ipv4.conf.default.accept_redirects = 0 
net.ipv6.conf.default.accept_redirects = 0

# Ignore Directed pings
net.ipv4.icmp_echo_ignore_all = 1
`
`sudo sysctl -p`
- [ ] spoofing
`sudo vi /etc/host.conf` put / edit 
`
order bind,hosts
nospoof on
`
- [ ] Harden PHP for security
`sudo vi /etc/php5/apache2/php.ini`
`
disable_functions = exec,system,shell_exec,passthru
register_globals = Off
expose_php = Off
magic_quotes_gpc = On

`
- [ ] firewall

## First connection on SSH :
check file syntax `sshd -t`
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
- [ ] Change pwd
- [ ] Install HTTP **(apache2)**
- [ ] Delete /apache2-default/ redirection
- [ ] Install PHP
- [ ] Install DataBase **(MariaDB)**
- [ ] Install DNS server
- [ ] Install Mail server
