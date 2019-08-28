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
- L'instal·lació de dos servidos web amb PHP i Apache per implementar un WordPress.
- Instal·lar un servidor de base de dades.

L'arquitectura que volem contruir serà la següent:

![alt text](../img/8.png "8")

### 2. Vagrant

Per començar a desenvolupar aquest projecte orientat a la pràctica he utilitzat un recurs molt innovador per crear, modificar i gestionar les meves màquines virtuals a partir de Virtual-Box, això ho he fet amb [Vagrant](https://www.conasa.es/blog/vagrant-la-herramienta-para-crear-entornos-de-desarrollo-reproducibles/).

![alt text](../img/Vagrant.png "Vagrant")

Per fer-ho primer he hagut de crear en una zona de proves amb 1 controlador, 1 servidor de carrega, 2 nodes webserver i 1 per fer l'implementació de la BBDD a partir del [fitxer de configuració](/annexos/#controllernode).

### 3.Creació de rols i configuració de màquina

Un cop hem pogut comprovar que les màquines han sigut creades segons els nostres fitxers *Vagrantfile* he tingut que [habilitar el SSH i l'autorització del usuari root](/annexos/#ssh-passwd) de forma remota per poder connectarnos amb Ansible amb el mateix ID a tots els nostres servidors.

Havent acabat la configuració prèvia de nostres maquines podem procedir a entrar dins del nostre entorn Ansible, no sense abans comprovant la correcta sincronització de data i hora i la disponibilitat dels nostres recursos, podem trobar més informació sobre les comandes bàsiques [aquí](/annexos/#comandasbasicas).

![alt text](../img/19.png "19")

Aquesta comprovació de data i hora la fem perquè encara que algunes aplicacions tolerim una petita diferencia horaria si es sobrepasa el límit podem tenir problemes d'incongruencies entre els nostres nodes, la forma més sencilla es utilitzan el NTP *Network Time Protocol*.

__Hosts del proyecte__

Dintre del fitxer `hosts` he afegit els meus servidors perquè Ansible els pugui controlar, juntament amb les serves varoables de grups y hosts.

Fitxer `/etc/ansible/hosts`

hosts.png

__Estructura del nostre sistema de fitxers__

estructurafinal.png

__Instal·lació del nostre balancejador de càrrega__

Per fer-ho he tingut que crear un rol anomenat `haproxy` on he posat el següent codi per instal·lar el HAProxy en el nostre servidor.

- Fitxer de configuració `loadbalancers.yml`:

```
---
- name: Servidor de càrrega (LoadBalancer)
  hosts: loadbalancers
  roles:
    - role: haproxy
...
```

loadbalancer1.png

[Més informació sobre l'instal·lació d'HAProxy.](../annexos/#loadbalancer)

Un cop tenim el HAProxy configurat només tenim que anar a la següent url per veure el panell de administració.

http://192.168.10.101/haproxy?stats

loadbalancer2.png

Com podem veure els nostres dos serveis web es troben _DOWN_ això es perquè encara no tenim cap servidor web configurat.

__Webservers i configuració dels servidors web__

Semblant a l'instal·lació del servidor de càrrega he creat un rol amb el nom de `apache` per poder configurar i administrar els nostres dos servidors de Apache.

- Fitxer de administració i instal·lació del rol Apache i PHP `webservers.yml`:

```
---
- name: Servidors web amb Apache
  hosts: webservers
  roles:
    - role: apache
    - role: php
...
```

webservers1.png

Comproven que càrrega els nostres llocs amb la pàgina per defecte de Apache:

webservers2.png

webservers3.png

Instal·lació de totes les tasques per poder configurar el nostre Apache:

webservers4.png

[Més informació sobre la configuració i instal·lació del nostres servidors Apache.](../annexos/#webserversapache)

Instal·lació del rol de PHP en el nostre servidor:

php1.png

[Configuració dels fitxers d'instal·lació de PHP.](../annexos/#php)

__Instal·lació i configuració de MySQL__

Per crear la nostra infraestructura amb WordPress es necessari tenir una base de dades instal·lada al notre servidor `192.168.10.10`.

* Utilitzarem el següent codi per poder instal·lar el nostre rol de **mysql**:

```
---

- name: Servidor Base de dades
  hosts: bdserver
  roles:
    -role: mysql
...
```

bbdd1.png

[Condifuració de la nostra bbdd.](../annexos/#bbdd)

__Instal·lació i configuració de WordPress__




