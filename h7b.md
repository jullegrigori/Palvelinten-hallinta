b) Oma moduli (iso tehtävä). Ratkaise jokin oikean elämän tai keksitty tarve omilla tiloilla/moduleilla. Voit käyttää Salttia tai muuta valitsemaasi
modernia keskitetyn hallinnan ohjelmaa. Esitä tulos viimeisellä opetuskerralla, 5-10 min. Live demo olisi kiva.

HomeAssistant-raspin etähallinta kotona, vanhemmilla ja uudelleenasennustilanteissa

```
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
```

Ajatuksena on tehdä oma 




Raportoi modulisi tarkoitus, koodi ja testit.

Hovimestari on syyllinen! Eli heti aluksi pitäisi selvitä, mitä hyötyä jutustasi on. Ja mikä se on!

Esitys on hyvä aloittaa lopputuloksesta ja hyödyistä
Työn weppisivulle taitoksen yläpuolelle (skrollaamatta näkyvään osaan) ainakin
Ruutukaappaus
Lisenssi
Yhden rivin selitys - mikä tämä on
(teknisissä ratkaisuissa, kuten tämä) Parilla sanalla, miten tämä on tehty
Näillä houkuttelet kävijät lukemaan ja asentamaan koko jutun
