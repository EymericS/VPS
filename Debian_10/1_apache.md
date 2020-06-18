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
  
  * 

## OTHER

`/etc/apache2/sites-available`
`/etc/apache2/sites-enabled`


  * indicate default index type file : `DirectoryIndex index.html index.php index.xhtml` *(around line 200)*
  
  ## Apache2 mods
  
  
  
  
  
  
