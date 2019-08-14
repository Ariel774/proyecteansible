# Desenvolupament del projecte

Per començar a desenvolupar aquest projecte orientat a la pràctica he utilitzat un recurs molt innovador per crear, modificar i gestionar les meves màquines virtuals a partir de Virtual-Box, això ho he fet amb Vagrant.

[¿Qué es Vagrant?](https://www.conasa.es/blog/vagrant-la-herramienta-para-crear-entornos-de-desarrollo-reproducibles/)

Per fer-ho primer he hagut de crear en una zona de proves amb 1 controlador i 2 nodes a partir del fitxer de configuració controller i el fitxer node 1-2.

Un cop hem pogut comprovar que les màquines han sigut creades segons els nostres fitxers *Vagrantfile* he tingut que <a>habilitar el SSH i l'autorització del usuari root<a> de forma remota.

Havent acabat la configuració prèvia de nostres maquines podem procedir a entrar dins del nostre entorn Ansible, no sense abans comprovant la correcta sincronització de data i hora i la disponibilitat dels nostres recursos.
