# Index

1. Origen d' Ansible<br>
2. ¿Qué es Ansible?<br>
3. Ansible Playbooks<br>
4. Iventaris<br>
  4.1 Hosts i grups<br>
  4.2 Hosts i variables<br>
  4.3 Organización de variables<br>
5. Rols e includes<br>
6. Ansible portat a la pràctica<br>
  6.1 Començant el projecte<br>
  6.2 Creació de rols i configuració de màquina<br>
  6.3 Webserver i configuració Apache<br>
  6.4 Instalació i configuració de un WordPress<br>
  6.5 Instalació i configuració de MySQL<br>
  
¿Origen d’ Ansible?
Va néixer de la necessitat de poder administrador diversos servidors...
¿Qué es Ansible?
Ansible es un software que permet l’automatització, aprovisionament, gestió i el desplegament de aplicacions en diferents servidors de forma simultània i paral·lela. 
Aquesta eina esta categoritzada com a una eina de orquestració.
Es una eina de codi obert, Open Source en la que actualment es troba treballant molta gent fet que el fa una eina actualitzada i segura, l’autor de Ansible es Michael DeHaan i té un repositori amb el codi de l’eina allotjada en un Github:
https://github.com/ansible/ansible
¿Com es connecta Ansible als diferents nodes per a poder gestionar-ho?
Ansible gestiona els diferents nodes associats a ell mitjançant SSH, l’únic requeriment que necessita Ansible es que el servidor remot tingui instal·lat el Python per a poder utilitzar-ho.
¿Com escrivint un projecte amb Ansible?
Utilitza YAML per a descriure les accions a realitzar y configurar les diferents tasques a fer per que aquestes es puguin propagar als diferents nodes.
¿Qué es YAML i com funciona? ***
2 - Disponibilitat:
En l’actualitat Ansible es distribueix en Fedora, Red Hat, Linux, CentOs, i Scientific Linux mitjançant els paquets EPEL (Extra Packages for Enterprise Linux).
A més dels SO anteriorment mencionats, aquesta eina també es troba distribuïda i es podem trobar des de un buscador de paquets: https://goo.gl/y6ad6g

