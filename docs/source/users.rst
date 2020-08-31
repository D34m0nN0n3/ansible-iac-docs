Создание локальных учетных записей в ОС CentOS/RHEL с помощью Ansible
=====================================================================
Роль для создания типовых учетных записей согласно типовым требования: *root, adminos, aminptk, adminvp0, adminvp1, adminvp2, smenaptk*. Актуализация аутентификационных данных. 

.. note:: **Задачи сгруппированы в блоки управления учетными записями (УЗ), для *root, adminos, adminptk* задачи разгруппированы и выполняются отдельно, для *adminvp[0,1,2], smenaptk* объединены в один блок. Выполнить блок можно указав тег или задав специальную переменную.**

.. attention::  **По умолчанию выполенние задач игнорируется.**

.. attention::  **SSH ключи и пароли передается как шифрованный секрет. Пароль для каждого сервера генерируется случайным образом.**

Дополнительные переменные
~~~~~~~~~~~~~~~~~~~~~~~~~
Для данного проекта зарезервированы следующие переменные приведенные в таблице:

.. table:: 

============================= =============================================================================================
Var                           INFO
============================= =============================================================================================
root_mgmt                     Включает управление УЗ *root'a*. 
root_pass                     Устанавливает пароль *root'у*, зависит от переменной. Обновится , если они отличаются.
adminos_mgmt                  Включает управление УЗ *adminos*.
adminos_pass                  Устанавливает пароль *adminos*, зависит от переменной. Обновится , если они отличаются.
adminos_key                   Сздает ключ авторизации *adminos*, зависит от переменной. Обновится , если они отличаются.
adminptk_mgmt                 Включает управление УЗ *adminptk*.
adminptk_pass                 Устанавливает пароль *adminptk*, зависит от переменной. Обновится , если они отличаются.
adminptk_key                  Сздает ключ авторизации *adminptk*, зависит от переменной. Обновится , если они отличаются.
adminvp_smena_mgmt            Включает управление УЗ *adminvp0, adminvp1, adminvp2, smenaptk*.
smenaptk_pass                 Устанавливает пароль *smenaptk*, зависит от переменной. Обновится , если они отличаются.
smenaptk_key                  Сздает ключ авторизации *smenaptk*, зависит от переменной. Обновится , если они отличаются.
adminvp0_pass                 Устанавливает пароль *adminvp0*, зависит от переменной. Обновится , если они отличаются.
lock_pass                     Блокирует или разблокирует УЗ *adminvp0*.
adminvp_pass                  Устанавливает пароль *adminvp[1,2]*, не обновляется при изменение переменной.
============================= =============================================================================================

.. attention::  В переменные устрановливающие пароли указываются хеши sha-512. Подробно описанно здесь: `how-do-i-generate-encrypted-passwords-for-the-user-module <https://docs.ansible.com/ansible/latest/reference_appendices/faq.html#how-do-i-generate-encrypted-passwords-for-the-user-module>`_.

----

При выполенние сценария автоматически генерируются правила `sudoers`, переменные для шаблона праведенны в таюлице ниже:

.. table:: 

============================= =============================================================================================
Var                           INFO
============================= =============================================================================================
sudo_services_drive           Список сервисов (служб) которыми можно управлять. 
sudo_services_boot            Список сервисов (служб) которые можно автоматически запускать.
srules_custom                 Дополнительные правила.
============================= =============================================================================================

Пример шаблона: ::

    #{{ ansible_managed }}
    Host_Alias SERVERS = 10.0.0.0/8
    Cmnd_Alias AGENTS = /usr/openv/netbackup/bin/bp.start_all, /opt/IBM/ITM/bin/itmcmd agent stop *, /opt/IBM/ITM/bin/itmcmd agent start *, /usr/bin/kesl-control --start-task 6, /usr/bin/kesl-control --app-info, /usr/bin/systemctl start klnagent64, /usr/bin/systemctl restart klnagent64, /usr/bin/systemctl stop klnagent64, /usr/bin/systemctl start kesl-supervisor, /usr/bin/systemctl restart kesl-supervisor, /usr/bin/systemctl stop kesl-supervisor
    Cmnd_Alias PROCESSES = /usr/bin/ps -[aefuxw]*, /bin/nice -n [-0-5] *, /bin/kill -s (TERM|KILL) [0-9]*, /usr/bin/kill -s (TERM|KILL) [0-9]*, /usr/bin/killall
    Cmnd_Alias NETWORKING = /sbin/route -n, /sbin/ifconfig [-a-z0-9]*, /bin/ping *, /usr/bin/host -(a|t) *, /usr/bin/nmtui, /sbin/iptables -[vnL]*, /sbin/iptables-save *, /usr/sbin/nft list ruleset, /usr/sbin/nft -s list ruleset *
    Cmnd_Alias SERVICES = /usr/bin/systemctl status *{% if sudo_services_drive is defined %}{%   for units in sudo_services_drive %}, /usr/bin/systemctl start {{ units }}, /usr/bin/systemctl stop {{ units }}, /usr/bin/systemctl restart {{ units }}{%   endfor %}{% endif %}{% if sudo_services_boot is defined %}{%   for units in sudo_services_boot %}, /usr/bin/systemctl enable {{ units }}, /usr/bin/systemctl disable {{ units }}{%   endfor %}{% endif %}, /usr/bin/systemctl reload
    Cmnd_Alias SOFTWARE = /usr/bin/yum, /usr/bin/dnf, /usr/bin/systemctl
    Cmnd_Alias SMENA =  /sbin/reboot, /sbin/shutdown -P +[0-9]+ "*", ! /usr/bin/bash
    Cmnd_Alias NROOT = /usr/bin/su [!-]*, ! /usr/bin/su *root*
    Cmnd_Alias DEBUG = /usr/bin/nmap, /usr/sbin/tcpdump
    Cmnd_Alias FILES = /usr/bin/ls, /usr/bin/cat, /usr/bin/grep, /usr/bin/egrep, /usr/bin/stat, /usr/sbin/lsof, /usr/bin/getfacl, /usr/bin/lsattr, /usr/bin/find, !/usr/bin/find *-exec*, !/usr/bin/find *-fprint*, !/usr/bin/find *-ok*
    Cmnd_Alias BIN = /usr/sbin/sosreport, /usr/bin/yum update, /usr/bin/dnf upgrade, ! /usr/bin/bash
    {% if srules_custom is defined %}{%   for rules in srules_custom %}Cmnd_Alias SRULES = {{ rules }}{%   endfor %}{% endif %}
    smenaptk  SERVERS = NOPASSWD: AGENTS, PROCESSES, NETWORKING, FILES, SERVICES, SMENA, NROOT, BIN{% if srules_custom is defined %}, SRULES{% endif %}
    adminvp0  ALL=(ALL)   NOPASSWD: PROCESSES, NETWORKING, FILES, SOFTWARE, DEBUG, !SERVICES
    adminvp1  ALL=(ALL)   NOPASSWD: PROCESSES, NETWORKING, FILES, SERVICES, DEBUG, NROOT, BIN
    adminvp2  ALL=(ALL)   NOPASSWD: PROCESSES, NETWORKING, FILES, SERVICES, DEBUG, NROOT, BIN

Теги
~~~~

.. table:: 

===================== ==================================================
Tag                   INFO
===================== ==================================================
root_mgmt             Запускае задачи для УЗ *root*.
adminos_mgmt          Запускае задачи для УЗ *adminos*.
vimrc_conf            Создает конфиг для Vim УЗ *adminos*.
tmux_conf             Создает конфиг для Tmux УЗ *adminos*.
adminptk_mgmt         Запускае задачи для УЗ *adminptk*.
smena_mgmt            Запускае задачи для УЗ *smenaptk*.
adminvp0_mgmt         Запускае задачи для УЗ *adminvp0*.
adminvp_mgmt          Запускае задачи для УЗ *adminvp[1,2]*.
sudoers_mgmt          Обновляет правила `sudoers`.
===================== ==================================================
