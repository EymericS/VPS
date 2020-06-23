# In Progress ( lots of stuff to undersand and apply )

# Postfix mail server

`sudo dpkg-reconfigure postfix`
[tuto](https://technique.arscenic.org/la-gestion-des-emails/postfix-serveur-smtp/article/installer-et-configurer-postfix)

## /etc/postfix/main.cd edit

* `myhostname` : indique le nom de la machine exploitant le système Postfix sous forme qualifiée
* `mydomain` : indique le domaine de rattachement de $myhostname
* `myorigin` : indique le domaine qui apparaît dans le courrier envoyé à partir de cette machine
* `mydestination` : indique les domaines pour lesquels cette machine délivrera le courrier localement
* `mynetworks_style` & `mynetworks` : indique les réseaux autorisés et des domaines autorisés pour le relaie du courrier des clients
* `relay_domains` : indique les destination relaie de courrier étranger (provenant de clients hors réseaux autorisés) seulement vers les destinations autorisées. 
* `relayhost` : indique la livraison via des passerelle de messagerie

## /etc/aliases edit
`
  postmaster: user1
  root: user1
`
after editing run : `newaliases`

## logs postfix

etc/syslog.conf
    mail.err                                   /dev/console
    mail.debug                                 /var/log/maillog
IMPORTANT : beaucoup d'implémentations de syslogd ne créent pas les fichiers. Vous devez les créer avant de (re)lancer syslogd.
IMPORTANT : beaucoup d'implémentations de syslogd ne créent pas les fichiers. Vous devez les créer avant de (re)lancer syslogd.


    # postfix check
    # egrep '(reject|warning|error|fatal|panic):' /fichier/journal

    La première ligne (postfix check) invite Postfix à rapporter les problèmes de permission/appartenance.

    La seconde ligne examine les problèmes rapportés par le logiciel de courrier et renvoie ceux concernant les relais et requêtes malformées. Ceci peut produire beaucoup de lignes. Vous pouvez appliquer d'autres filtres pour éliminer les informations inintéressantes.



