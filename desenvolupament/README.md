# Desenvolupament del projecte

##Objectiu

- En el nostre projecte farem l'instalació d' un balancejador de carrega, l'instalació de dos servidors web amb PHP i Apache en el que executarem un WordPress.

Per començar a desenvolupar aquest projecte orientat a la pràctica he utilitzat un recurs molt innovador per crear, modificar i gestionar les meves màquines virtuals a partir de Virtual-Box, això ho he fet amb Vagrant.

fotovagrant.png

[¿Qué es Vagrant?](https://www.conasa.es/blog/vagrant-la-herramienta-para-crear-entornos-de-desarrollo-reproducibles/)

Per fer-ho primer he hagut de crear en una zona de proves amb 1 controlador i 2 nodes a partir del [fitxer de configuració controller i el fitxer node 1-2](/annexos/#controllernode).

Un cop hem pogut comprovar que les màquines han sigut creades segons els nostres fitxers *Vagrantfile* he tingut que [habilitar el SSH i l'autorització del usuari root](/annexos/#ssh-passwd) de forma remota.

Havent acabat la configuració prèvia de nostres maquines podem procedir a entrar dins del nostre entorn Ansible, no sense abans comprovant la correcta sincronització de data i hora i la disponibilitat dels nostres recursos, podem trobar més informació sobre les comandes bàsiques [aquí](/annexos/#comandasbasicas).

19.png

Aquesta comprovació de data i hora la fem perquè encara que algunes aplicacions tolerim una petita diferencia horaria si es sobrepasa el límit podem tenir problemes d'incongruencies entre els nostres nodes, la forma més sencilla es utilitzan el NTP *Network Time Protocol*.


