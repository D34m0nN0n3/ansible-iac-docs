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
  cockpit
  users
  mpuser

Ссылки на дополнительную докумкнтацию:
--------------------------------------

* `Ansible installation guide <https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html>`_.
* `Ansible Documentations <https://docs.ansible.com>`_.
* `Ansible tags <https://docs.ansible.com/ansible/latest/user_guide/playbooks_tags.html>`_.
* `Connection methods <https://docs.ansible.com/ansible/latest/user_guide/connection_details.html>`_.
* `Ansible passing sudo <https://8gwifi.org/docs/ansible-sudo-ssh-password.jsp>`_.
