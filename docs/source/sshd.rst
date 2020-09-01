Настройка SSHD на CentOS/RHEL с помощью Ansible
===============================================
Роль для настройки SSH службы. 

Пакеты устанавливаемы на RHEL7:
  * cockpit
  * cockpit-ws
  * cockpit-dashboard
  * cockpit-doc
  * cockpit-packagekit
  * cockpit-subscriptions
  * subscription-manager-cockpit
  * cockpit-docker
  * cockpit-composer
  * cockpit-system
  * cockpit-storaged
  * cockpit-pcp
  * cockpit-tests
  * policycoreutils-python

Пакеты устанавливаемы на RHEL8:
  * cockpit
  * cockpit-ws
  * cockpit-dashboard
  * cockpit-doc
  * cockpit-packagekit
  * subscription-manager-cockpit
  * cockpit-podman
  * cockpit-composer
  * cockpit-system
  * cockpit-storaged
  * cockpit-pcp
  * cockpit-session-recording
  * policycoreutils-python-utils

Дополнительные переменные
~~~~~~~~~~~~~~~~~~~~~~~~~
Для данного проекта зарезервированы следующие переменные приведенные в таблице ниже:

.. table:: 

============================= ==================================================================
Var                           INFO
============================= ==================================================================
websm_port                    Задает альтернативный порт для доступа к UI. По умолчанию `3389`. 
============================= ==================================================================

Теги
~~~~

.. table:: 

=============== ====================================
Tag             INFO
=============== ====================================
cockpit         Устанавливает интерфейт управления.
=============== ====================================
