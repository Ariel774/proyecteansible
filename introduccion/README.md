# Index

1. [Origen d' Ansible](#origen)<br>
2. [¿Qué es Ansible?]<br>
3. [Ansible Playbooks]<br>
4. [Iventaris]<br>
  4.1 [Hosts i grups]<br>
  4.2 [Hosts i variables]<br>
  4.3 [Organización de variables]<br>
5. [Rols e includes]<br>
6. [Ansible portat a la pràctica]<br>
  6.1 [Començant el projecte]<br>
  6.2 [Creació de rols i configuració de màquina]<br>
  6.3 [Webserver i configuració Apache]<br>
  6.4 [Instalació i configuració de un WordPress]<br>
  6.5 [Instalació i configuració de MySQL]<br>

<a name="origen"></a>  
## 1. Origen d’ Ansible

Va néixer de la necessitat de poder administrador diversos servidors...

## 2. ¿Qué es Ansible?

Ansible es un software que permet l’automatització, aprovisionament, gestió i el desplegament de aplicacions en diferents servidors de forma simultània i paral·lela. 

**Aquesta eina esta categoritzada com a una eina de orquestració.**

Es una eina de codi obert, Open Source en la que actualment es troba treballant molta gent fet que el fa una eina actualitzada i segura, l’autor de Ansible es Michael DeHaan i té un repositori amb el codi de l’eina allotjada en un Github:

https://github.com/ansible/ansible

¿Com es connecta Ansible als diferents nodes per a poder gestionar-ho?

Ansible gestiona els diferents nodes associats a ell mitjançant SSH, l’únic requeriment que necessita Ansible es que el servidor remot tingui instal·lat el Python per a poder utilitzar-ho.

¿Com escrivint un projecte amb Ansible?

Utilitza YAML per a descriure les accions a realitzar y configurar les diferents tasques a fer per que aquestes es puguin propagar als diferents nodes.

### Disponibilitat

En l’actualitat Ansible es distribueix en Fedora, Red Hat, Linux, CentOs, i Scientific Linux mitjançant els paquets EPEL (Extra Packages for Enterprise Linux).
A més dels SO anteriorment mencionats, aquesta eina també es troba distribuïda i es podem trobar des de un buscador de paquets: https://goo.gl/y6ad6g

6.png

En el nostre cas utilitzaren una maquina virtual i descarregarem l’eina més actual per comandes.
La podem trobar per dispositius Mac no obstant això **no està disponible per Windows**.

### Arquitectura de Ansible.

Com abans hem comentat Ansible es una eina que serveis per instal·lar, configurar i manejar diferents servidor de forma paral·lela, tenim que diferenciar que n’hi han dos tipus.

- El controlador: Aquesta es la màquina des de la que comença tot el maneig dels diferents servidor els quals d’alguna forma ‘’penjent d’aquest’’, en aquest punt comença l’orquestació.

- Node: Es maneja per el controlador mitjançant una connexió SSH.

arquitectura.png

La màquina que realitza la tasca de controlador reconeix als altres nodes mitjançant un inventari, que, per organitzar-ho fa un desplegament de mòduls sobre el protocol SSH, aquest desplegament fa que els mòduls desplegats no siguin controlats per el controlador, si no que **es la mateixa màquina remota la que s’encarrega de fer-ho** d’aquesta manera la **màquina local no consumeix recursos ni processos executant-se en segon pla.**

Una gran diferencia que podem trobar amb altres programes semblants com Chef o Puppet es que Ansible utilitza una arquitectura **sense agents**, l’arquitectura basada en agents, té com a finalitat instal·lar localment un procés de comunicació amb la màquina que fa de controlador, amb la nova arquitectura de Ansible sense agents, els nodes no es necessiten instal·lar ni executar ja que aquests mòduls son independents, aquesta arquitectura redueix la carrega de xarxa i prevé l’ús de control més concretes i potents per part del servidor.

### 4. Inventaris

Dintre d'Ansible existeixen diverses formes de indicar-li al software les tasques i/o gestions a orquestar que volem fer.

La més fàcil es ficar les nostres màquines nodes al **inventari que Ansible té dintre del nostre sistema**, això es pot localitzar dintre de `/etc/ansible/hosts`.

Com podem veure dintre del fitxer podem afegir de diverses formes els nostres hosts, partint desde un nom de domini, ip, ficar-los dintre d'un grup, delimitant-los amb un header per crear grups.

11.png

Per posar els nostres dos nodes dintre del nostre inventari un ficarem de la següent forma:

12.png



### 6. Ansible portat a la pràctica. (DESENVOLUPAMENT)

L'estructura que utilitzarem per fer totes les nostres proves en Ansible serà la seguent:

8.png



