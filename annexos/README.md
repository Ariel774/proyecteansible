# Instalació de Ansible per Ubuntu:

## Instalació en Linux.
Per començar tenim que instal·lar el software de Ansible, per portar-ho a terme llançaren les següents comandes:

`$ sudo apt-add-repository ppa:ansible/ansible`

`$ sudo apt-get Update`

`$ sudo apt-get install ansible`

Al llençar la comanda “sudo apt-get install ansible” ens donarà un error amb el Ubuntu 18.04 per tractar de solventar-ho tenim que llençar la comanda següent

`$ sudo add-apt-repository universe`

## Configuració de les nostres màquines mitjançant VAGRANT

En el meu cas per a poder gestionar de forma molt més senzilla i ràpida totes les màquines virtuals he fet us de l’eina anomenada Vagrant, ja que no només em deixa la possibilitat de poder instal·lar cuántes màquines vulgui si no que puc implementar l’Ansible de forma més sencilla i ràpida, a més de poder aprofitar el codi per llençar els nodes que implementaré després.

Per començar, en aquest apartat podem veure el fitxer empleat per la configuració de la nostra maquina principal Ansible, podem observar que utilitzen una versió de Ubuntu 16.04, amb una xarxa privada amb l’IP 192.168.10.100, una carpeta compartida Shared que s’ubicarà en l’arrel de el nostre Vagrantfile, memòria ram i CPU. 

4.png

Si observen el fitxer veurem que hi ha una configuració amb el path “config.sh” això ho utilitzarem per instal·lar el Ansible de forma automàtica a la nostra màquina virtual.

5.png

I iniciem el nostre servidor controlador que serà l’encarregat de gestionar els altres nodes, carreguem la configuració del fitxer amb la comanda `vagrant up`.

1.png
2.png

I ara per veure si la nostra màquina s’ha configurat correctament fem un SSH cap a l’IP del nostre servidor.

3.png 

<a name"ssh-passwd"></a>
## Habilitació del SSH i contrasenya per la correcta gestió de Ansible

Un dels problemes que té l’administració remota es la continua petició de les credencials alhora d’introduir una comanda de Ansible aquesta tasca pot ser molt feixuga si tenim molts nodes no volem que sempre ens demani la contrasenya, així que per obviar-lo haurem d’ habilitar per el nostre node principal la no autorització i copiar de la contrasenya root dels altres servidores, d’aquesta forma farem Ansible pugui accedir de forma correcta:

Primer de tot autoritzarem l’autorització per ssh del usuari root dintre del fitxer `/etc/ssh/sshd_config`, canviarem el prohibit password per **yes**:

7.png

Per tal de poder obtenir les mateixes credencials de root en tots els nodes utilitzarem la següent comanda que ens crearà una nova clau:

`$$ ssh-keygen –t rsa` (Aquesta comanda el que fa es generar unes claus per el ssh-copy-id)

10.png

`$vagrant@cotroler: ssh-copy-id root@192.168.10.101`

També cal tenir present que no sempre realitzarem tasques com a root de forma que també copiarem la contrasenya del usuari, en aquest cas serà el de Vagrant.

`$vagrant@cotroler: ssh-copy-id vagrant@192.168.10.101`





