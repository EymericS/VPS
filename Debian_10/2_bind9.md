# DNS Server

As a DNS server, tranlate from IP to Domain and vice versa.

## Bind9 command

* config file at `/etc/bind/named.conf`
 * prevent to be an free open DNS relay : add `allow-recurtion ( localhost; );` onto `{ ... }`in **/etc/bind/named.conf.options** or directly in **/etc/bind/named.conf**

## Create new zone

* zone declaration :
  * at `/etc/bind/named.conf.local`
  * ````
    zone "domain.name" {
      type master;
      file "/etc/bind/db.domain.name";
    };
  ````
  * create zone description file : **/etc/bind/db.domain/name** and file with ( for exemple ) : 
  ````
  $ttl 86400
  domain.name.       IN      SOA     ksXXXXX.kimsufi.com. webmaster.domain.name. (
                                      2006121903
                                      21600
                                      3600
                                      604800
                                      86400 )
  domain.name.    IN      NS             ksXXXXX.kimsufi.com.
  domain.name.    IN      NS             ns.kimsufi.com.
  domain.name.    IN      MX              10 mail.test1.com.
  domain.name.    IN    A           xxx.xxx.xxx.xxx
  Server        IN    A        xxx.xxx.xxx.xxx
  www        IN    A           xxx.xxx.xxx.xxx
  mail        IN    A           xxx.xxx.xxx.xxx
  smtp        IN    A           xxx.xxx.xxx.xxx
  pop         IN    A           xxx.xxx.xxx.xxx
  pop3        IN    CNAME        Server
  imap        IN    A           xxx.xxx.xxx.xxx
  sql        IN    A           xxx.xxx.xxx.xxx
  mysql        IN    A           xxx.xxx.xxx.xxx
````
  
  
  
