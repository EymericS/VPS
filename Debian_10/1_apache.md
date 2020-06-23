# Web server

> * apache2 are the must used http server on server. Lot of doc available on the net.
> * ability of virtual hosting to put several web site onto one server.
> * domain name are convert to IP by DNS, but the HTTP Header always contain initial domain name.

## Apache2 tools

* disable / enable launch at start : `~$ sudo systemctl [disable | enable] apache2`
* stop / start / restart / reload config : `~$ sudo systemctl [stop | start | restart | reload] apache2`
* apache used version : `~$ sudo apache2ctl -v`
* apache config test : `~$ sudo apache2ctl -t`
* apache vhost config test : `~$ sudo apache2ctl -t -D DUMP_VHOSTS`
* see wich module are currently load : `~$ sudo apache2ctl -M`
* disable / enable site configuration : `~$ sudo [a2ensite | a2dissite]`
* disable / enable service configuration : `~$ sudo [a2enconf | a2disconf]`
* disable / enable module configuration : `~$ sudo [a2enmod | a2dismod]`

## Apache2 config

* `/etc/apache2/apache2.conf` : 
  * check apache2 user and group, need to be `User www-data` and `Group www-data` *(around line 115)*
  * include the virtual host configurations : check the line `Include /etc/apache2/sites-enabled/[^.#]*` exist *(at the end)*
  
## VHost

### Personnal user website

* edit user creation skeleton (case 1):
  * `~$ sudo mkdir /etc/skel/public_html`
  * `~$ sudo mkdir /etc/skel/logs`
  * `~$ sudo echo " <h1>New peronnal website created</h1> " > /etc/skel/public_html/index.html`
* add new user :
  * `~$ sudo useradd -g www-data -m test1`
* allow unix user to share contents from his personnal home (case 2):
    * `~$ cd "personal/directory/home"`
    * `~$ mkdir public_html`
    * `~$ echo 'My personnal website' > public_html/index.html`
    * `~$ chmod -R 755 public_html`
    * `~$ sudo a2enmod userdir`
    * `~$ sudo systemctl reload apache2`
    
  > The message **My personnal website** available on http://domain/~unix-username
  
  > By default php file interpretation are disable : comment the right line in `/etc/apache2/mods-available/php7.x.conf`
  
### Website VHost

* create directory : `~$ sudo mkdir /var/log/apache2/exemple.tld`
* create file : `~$ sudo touch /etc/apache2/sites-available/exemple.tld.conf`
``
  <VirtualHost *:80>
        ServerAdmin webmaster@localhost
        ServerName www.exemple.tld
        ServerAlias exemple.com
        DocumentRoot /var/www/exemple.tld/
		
        <Directory /var/www/exemple.tld/>
                AllowOverride all         # permitte the use of .htaccess
                Require all granted       # allow all visitor
                Options -Indexes -Includes -ExecCGI +FollowSymlinks
                    # -Indexes (disable): open as file manager if no idex found
                    # -Inlcudes (disable): allow inclusion
                    # -ExecCGI (disable): allow CGI script
                    # +FllowSymlinks (enable): if a dir is a symbol link, follow the link ( enable URL rewrite )
        </Directory>

        ErrorLog /var/log/apache2/exemple.tld/error.log
        CustomLog /var/log/apache2/exemple.tld/access.log combined

        LogLevel warn        # Possible values include: debug, info, notice, warn, error, crit, alert, emerg.

</VirtualHost>
``
* enable new config : `~$ sudo a2ensite exemple.tld`
* reload apache2 : `~$ sudo systemctl reload apache2`
	
## HTTPS with TLS(SSL) and Certbot

### TLS

* Enable TLS mod on apache2 : `~$ sudo a2enmod ssl`
* Make change effective : `~$ sudo systemctl restart apache2`

### Certbot

* Install : `~$ sudo apt-get install certbot python-certbot-apache`
* Generate certificate : `~$ sudo certbot --apache` ( better secure to enable force https redirection )
	* List existing certificate : `~$ sudo certbot certificates`
		* to add many domain on one certif add them in same line : `www.domain.tld domain.tld`
		* or : `~$ certbot --expand -d existing.com -d example.com -d newdomain.com`
	* Renew certificate : `~$ sudo certbot renew`
	* Delete certificate :
		* Disable : `~$ sudo a2dissite exemple.tld-le-ssl
		* Revoke : `~$ sudo certbot revoke --cert-path /etc/letsencrypt/live/CERTNAME/fullchain.pem`
		* Delete : `~$ sudo certbot delete --cert-name example.tld`
	
## OTHER
* indicate default index type file : `DirectoryIndex index.html index.php index.xhtml` *(around line 200)*
  
## Apache2 mods
