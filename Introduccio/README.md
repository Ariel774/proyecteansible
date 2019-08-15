# Index

1. [Origen d' Ansible](#origen)<br>
2. [¿Qué es Ansible?](#ansible)<br>
3. [Ansible Playbooks](#playbooks)<br>
  3.1 [Mòduls PAT, usuaris i grups](#moduls)<br>
  3.2 [Arxius i directoris]
  3.3 [Crones]
  3.4 [Playbooks i YAML]
  3.5 [Estructura de un Playbook]
  3.6 [Hosts i usuaris]
  3.7 [Handlers]
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


<a name="ansible"></a>  
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


<a name="playbooks"></a>  
## 3. Ansible Playbooks

<a name="moduls"></a>  
### 3.1 Mòdulos PAT, usuaris i grups

__Mòduls - Serveïs__

En Ansible per poder utilitzar un dels seus mòduls que venem predefinits tenim que fer us del paràmetre `-m`.
Alguns d'aquests mòduls podem ser **yum, apt, o service** això ens servirà per instalar els nostres programes als nostres diferents nodes.

En aquest sencill exemple procedirem a instalar el paquet o mòdul NTP.

`$ansible all -b -m apt -a "name=ntp state=installed"`

22.png

Com s' observa en la captura comproven que en el node amb l'IP 192.168.10.101 el pàquet NTP ja es trova instal·lat, en canvi en la IP 192.168.10.102 encara no el té, Ansible té l'avantatge que comprova el servidor penjant que no tingui el mòdul i l'instal·la sense donar cap problema de tornar a reinstalar el mòdul un altre cop per el servidor.

* Podem desglossar la comanda de la següent manera:
 * "-a" En aquest paràmetre procedirem a pasar el paquet (name) juntament amb l'estat (state).
 * "-b" L'indiquem que volem executar l'ordre com a super usuari (sudo).
 * "-m" Es el mòdul en cuestió.

D'aquesta forma ens evitem tenir que anar a cada servidor fer un SSH i instal·lar el paquet.

Ara comproven que segons Ansible el paquet NTP es trova en estat **SUCCESS** que significa que no hi ha hagut cap canvi en les màquines i el mòdul NTP té un **state=installed** correcte.

Si canviem l' *state* per "name=ntp **state=absent"** comprovaren que l'output és que ha eliminat el mòdul, com si es tractès d'un `remove`.

24.png

Un cop tenim el nostre pàquet NTP instal·lat ja podem procedir a comprovar el seu "Status" amb la comanda `$ansible all -b -a "service ntp status`.

25.png

__Usuaris i grups__

Gràcies a Ansible, ara remotament podem administrar, gestionar, crear i modificar usuaris i grups desde el nostre node principal controller, per exemple si nosaltres volguessim afegir un grup anomenat "ASIX" ho fariem amb la següent comanda amb el mòdul "group":

* `$ansible all -b -m group -a "name=asix state=present"`(En aquest cas el **PRESENT** no vol dir instalar, si no que estigui present).

26.png

En la captura es pot observa que Ansible després de crear el grup també et diu el nom d'aquest juntament amb el seu GID, a més he posat una captura amb les dues comandes dues vegades perquè es pugui veure com en la primera part es detecta un canvi i en la segona ens dona un **SUCCESS** sense cap modificació.

Si ara volem crear un usuari dintre d'un grup, i al mateix temps crear la seva home, deurient de fer-ho de la següent forma amb el mòdul "user":

* `$ansible all -b -m user -a "name=ariel group=asix createhome=yes"`

27.png

De la mateixa forma que amb el grup això també ens dona un output amb les diferents variables que tenim del nostre usuari, gid, home i grup.

Comproven que l'usuari existeix com a tal:

28.png

Com observen ha creat l'usuari en el servidor amb l'IP acabada en .101, però de la mateixa forma també ho farà en l'altre.

Més informació sobre els usuaris i grups [aqui](https://docs.ansible.com/ansible/latest/modules/user_module.html)

__Arxius i directoris__

Aquest mòdul es un dels més utilitzats en l'actualitat, ja que degut a que nosaltres podem tenir diverses configuracions de Apache, PHP, MySQL... volem mantenir un mateix mòdul que estigui relacionat amb el mateix sistema de arxius i directoris d'aquesta manera eviten possibles incongruencies durant la creació dels directoris o fitxers.

* La comanda per veure l' **ESTAT** del fitxer o directori en questió es la següent:

 * `$ansible all -b -m stat -a "path=/etc/passwd"`

29.png

Mitjançant aquesta comanda podem observa el path del fitxer, si es executable, la seva mida, i moltes altres caràcteristiques d'aquest.

* Per **COPIAR** un fitxer partint d'un origen cap a un destí tenim que emplear aquesta linia de codi:

 * `$ansible all -b -m copy -a "src=/etc/hosts dest=/home/ariel/hosts`
 
30.png

Com observem es pot veure la mida del fitxer, el seu propietari i la destinació d'aquest.

**Important: si al paràmetre src posem una barra '/' al final, només copiarà els fitxers que estiguin dintre del directori cap al destí per el que la carpeta en si no es copiarà**

Ara utilitzarem el mòdul anometat **Fetch** que fa el mateix que el copy però descarregar els fitxers cap al nostre controlador.

* Aquesta comanda serveix per **DESCARREGAR** fitxers o directoris, i té el gran avantatge que encara que nosaltres descarreguessim fitxers de molts nodes **no els sobreescriurà**.

 * `$ansible all -b -m fetch -a "src=/home/ariel/hosts dest=/home/vagrant"
 
 31.png

Com podem observar ens crea dos directoris amb l'IP dels nostres servidors.

Per la creació modificació de fitxers i carpetes, juntament amb altres paràmetres d'aquests utilitzarem el mòdul "FILE".

* En aquest petit exemple crearem un **FITXER** amb els permissos 644.

 * `$ansible all -b -m file -a "dest=/home/ariel/prova1 mode=644 state=touch"`
 
 32.png

* Per crear una **CARPETA** utilitzarem la següent comanda.

 * `$ansible all -b -m file -a "dest=/home/ariel/ASIX mode=644 state=directory"`
 
 33.png

Comproven que existeixen:

34.png

* Si volem eliminar un fitxer o carpeta nomès deuriem de posar en **state=absent**.

 * `$ansible all -b -m file -a "dest=/home/ariel/ASIX mode=644 state=absent"`

35.png

Per veure més informació sobre els paràmetres a posar, [aqui](https://docs.ansible.com/ansible/latest/modules/file_module.html).

## 4. Inventaris

Dintre d'Ansible existeixen diverses formes de indicar-li al software les tasques i/o gestions a orquestar que volem fer.

La més fàcil es ficar les nostres màquines nodes al **inventari que Ansible té dintre del nostre sistema**, això es pot localitzar dintre de `/etc/ansible/hosts`.

Com podem veure dintre del fitxer podem afegir de diverses formes els nostres hosts, partint desde un nom de domini, ip, ficar-los dintre d'un grup, delimitant-los amb un header per crear grups.

11.png

Per posar els nostres dos nodes dintre del nostre inventari un ficarem de la següent forma:

12.png



### 6. Ansible portat a la pràctica. (DESENVOLUPAMENT)

L'estructura que utilitzarem per fer totes les nostres proves en Ansible serà la seguent:

8.png
