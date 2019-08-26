# Desenvolupament del projecte

1. [Objectiu]<br>
2. [Vagrant]<br>
3. [Creació de rols i configuració de màquina]<br>
4. [Webserver i configuració Apache]<br>
5. [Instalació i configuració de un WordPress]<br>
6. [Instalació i configuració de MySQL]<br>

## 1. Objectiu

Per poder desenvolupar el nostre projecte farem ús de Vagrant per crear el nostre entorn de desenvolupament.

Amb Ansible farem:

- L'implementació d' un servidor de carrega.
- L'instalació de dos servidos web amb PHP i Apache per implementar un WordPress.
- Instalar un servidor de base de dades.

### Vagrant

Per començar a desenvolupar aquest projecte orientat a la pràctica he utilitzat un recurs molt innovador per crear, modificar i gestionar les meves màquines virtuals a partir de Virtual-Box, això ho he fet amb Vagrant.

fotovagrant.png

[¿Qué es Vagrant?](https://www.conasa.es/blog/vagrant-la-herramienta-para-crear-entornos-de-desarrollo-reproducibles/)

Per fer-ho primer he hagut de crear en una zona de proves amb 1 controlador, 1 servidor de carrega, 2 nodes webserver i 1 per fer l'implementació de la BBDD a partir del [fitxer de configuració controller i el fitxer node 1-2](/annexos/#controllernode).
-
Un cop hem pogut comprovar que les màquines han sigut creades segons els nostres fitxers *Vagrantfile* he tingut que [habilitar el SSH i l'autorització del usuari root](/annexos/#ssh-passwd) de forma remota.

Havent acabat la configuració prèvia de nostres maquines podem procedir a entrar dins del nostre entorn Ansible, no sense abans comprovant la correcta sincronització de data i hora i la disponibilitat dels nostres recursos, podem trobar més informació sobre les comandes bàsiques [aquí](/annexos/#comandasbasicas).

19.png

Aquesta comprovació de data i hora la fem perquè encara que algunes aplicacions tolerim una petita diferencia horaria si es sobrepasa el límit podem tenir problemes d'incongruencies entre els nostres nodes, la forma més sencilla es utilitzan el NTP *Network Time Protocol*.


