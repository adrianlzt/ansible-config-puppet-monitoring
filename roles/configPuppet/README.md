Role Name
========

Este módulo genera los 'own facts' siguiendo los parámetros pasados.
También se encarga de actualizar puppet a la última versión.
Por último ejecuta puppet agent para puppetizar la máquina.

Podemos hacer uso de los tags para restringir que parte queremos ejecutar: conf, package, puppet.

En conf se ejecutará todas las acciones para generar los fichero de los facts en /etc/facter/facts.d
En caso de que la máquina no estuviese puppetizada, se moverá el directorio /etc/nrpe.d a /etc/nrpe.backup

Package actualizará que el paquete puppet está actualizado.

Puppet ejecutará: puppet agent -t --server={{ puppet_server }}

Requirements
------------

Este módulo es necesario ejecutarlo con sudo.

Role Variables
--------------

Variables definidas en defaults/main.yml:
facter_dir: /etc/facter/facts.d
puppet_server: puppet.ejemplo.com
monitoring_activated: true

Estas variables en principio no necesitan modificarse.


Variables que deben definirse obligatoriamente al declarar el rol:
project - proyecto al que pertenece la máquina
monitoring_env - entorno de monitorización donde configurar la máquina

Variables no obligatorias específicas por hosts, deben definirse en .ansible/hosts:
hostgroup - lista separada por comas de los hostgroups a los que pertenece la máquina
interface - interface de red a través de la que recibirá la máquina los chequeos (solo necesario si no es eth0)
vip - lista separada por comas de VIPs que tiene configurada la máquina


Dependencies
------------


Example Playbook
-------------------------

- hosts: pre
  sudo: True
  gather_facts: False
  roles:
    - { role: configPuppet, project: 'dSN-Tools', monitoring_env: 'pre' }


License
-------

BSD

Author Information
------------------

Adrián López
