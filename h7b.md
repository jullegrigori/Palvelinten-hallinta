b) Oma moduli (iso tehtävä). Ratkaise jokin oikean elämän tai keksitty tarve omilla tiloilla/moduleilla. Voit käyttää Salttia tai muuta valitsemaasi
modernia keskitetyn hallinnan ohjelmaa. Esitä tulos viimeisellä opetuskerralla, 5-10 min. Live demo olisi kiva.

##HomeAssistant-raspin hallinta##
Tarkoitus on luoda hallintamahdollisuus kotona olevaan raspi-debianiin (ja vanhemmilla). Tulevaisuudessa tarkoitus lisätä mm. config-tiedostojen backup ja palautus.

Aluksi pitää asentaa Home Assistantin dokumentaation mukaiset 

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
      
'ufw allow 9777/tcp':
cmd.run:
    - unless: "sudo ufw status verbose|grep '^9777/tcp '"
```


SSH-yhteyden muodostaminen onnistuu nyt näin:
ssh -p 9777 gri@XX.XX.XX.XX



