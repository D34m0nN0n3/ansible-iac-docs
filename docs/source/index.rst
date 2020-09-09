Проект по базовой настройке операционных систем RHEL/CentOS.
============================================================

Данная документация описывает параметры при использование Ansible Roles для базовой настройки серверов на базе операционных систем Red Hat.
Роли содержат сценарии по автоматизации ручных операций. За счет автоматизации уменьшаются время и трудозатраты на подготовку ПТК, снижаться риск влияния “человеческого фактора”. 

Исходный код сценариев находится по адресу: `https://github.com/D34m0nN0n3/ansible-iac <https://github.com/D34m0nN0n3/ansible-iac>`_.

.. toctree::
   :maxdepth: 2
   :caption: Contents:

  intro
  ntp
  auditd
  sysconfig
  sshd
  cockpit
  users
  mpuser
  firewall
  selinux
  itma
  ntbackup
  satellite
  
.. toctree::
   :maxdepth: 1
   :caption: Ссылки на дополнительную докумкнтацию
  finale
