# Instalació de Ansible per Ubuntu:

## Instalació en Linux.
Per començar tenim que instal·lar el software de Ansible, per portar-ho a terme llançaren les següents comandes:

`$ sudo apt-add-repository ppa:ansible/ansible`

`$ sudo apt-get Update`

`$ sudo apt-get install ansible`

Al llençar la comanda “sudo apt-get install ansible” ens donarà un error amb el Ubuntu 18.04 per tractar de solventar-ho tenim que llençar la comanda següent

`$ sudo add-apt-repository universe`
