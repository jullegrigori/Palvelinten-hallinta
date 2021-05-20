b) Oma moduli (iso tehtävä). Ratkaise jokin oikean elämän tai keksitty tarve omilla tiloilla/moduleilla. Voit käyttää Salttia tai muuta valitsemaasi
modernia keskitetyn hallinnan ohjelmaa. Esitä tulos viimeisellä opetuskerralla, 5-10 min. Live demo olisi kiva.

## HomeAssistant-raspin hallinta ##
Tarkoitus on luoda hallintamahdollisuus kotona olevaan raspi-debianiin (ja vanhemmilla). Tulevaisuudessa tarkoitus lisätä mm. config-tiedostojen backup ja palautus.

Aluksi loin ssh-konfigurointitiedoston minionilla, jossa ssh konfiguroitu porttiin 9777 ja kopioin sen masterille:

```
$ sudo nano /etc/ssh/sshd_config

#       $OpenBSD: sshd_config,v 1.103 2018/04/09 20:41:22 tj Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/bin:/bin:/usr/sbin:/sbin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options override the
# default value.

Port 9777
#AddressFamily any

...

```


Sitten Home Assistantin dokumentaation mukaiset esivaatimukset asentumaan ja mm. ufw, git ja tree. Sitten ufw:lle portti auki ja äsken luotu ssh-konffitiedosto minionille.

```
Masterilla:
/srv/salt/homeassistant$ sudoedit apps.sls

apps:
  pkg.installed:
    - pkgs:
      - tree
      - whois
      - bash 
      - curl
      - git 
      - jq 
      - avahi-daemon
      - dbus
      - apparmor-utils
      - network-manager
      - apt-transport-https
      - ca-certificates
      - socat
      - software-properties-common
      - ufw
      - openssh-server
      
'ufw allow 9777/tcp':
cmd.run:
    - unless: "sudo ufw status verbose|grep '^9777/tcp '"
    
/etc/ssh/sshd_config:
  file.managed:
    - source: salt://ssh/sshd_config

```



SSH-yhteyden muodostaminen onnistuu nyt näin:
ssh -p 9777 gri@XX.XX.XX.XX

Dockerin asennus onnistuu esim näin:
sudo curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh


(JATKUU)



## Lähteet ##

https://terokarvinen.com/2021/configuration-management-systems-palvelinten-hallinta-ict4tn022-spring-2021/


