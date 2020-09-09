Использование сценариев Ansible
===============================
* Прежде чем запускать сценарий на выполнение необходимо составить файл инвентаризации в котором прописываются целевые узлы и переменные.

Пример файла инвентаризации:

    # Переменные которые необходимо заменить на свои значения указаны в '< >', значения указываются без них. 
    # Все узлы объединяются в группы ИС/АСУ.
    # Данный фаил формируется в формате INI.
    [all:vars]
    # Список переменных.
    root_mgmt=true
    root_pass=<sha-256>
    ipv6_grub_disable=true
    ntp_servers=[ '10.248.7.3','10.248.7.4' ]
    ...
    и т. д.
    
    # Метод подключения к узлам для запуска сценария.
    ansible_connection=ssh
    
    [<group_hosts_name>]
    <host_name> ansible_ssh_host=<host_ip> ansible_ssh_user=<user_name_for_connect>
    <host_name> ansible_ssh_host=<host_ip> ansible_ssh_user=<user_name_for_connect>
    <host_name> ansible_ssh_host=<host_ip> ansible_ssh_user=<user_name_for_connect>
    
    [<group_hosts_name>]
    <host_name> ansible_ssh_host=<host_ip> ansible_ssh_user=<user_name_for_connect>
    <host_name> ansible_ssh_host=<host_ip> ansible_ssh_user=<user_name_for_connect>
    <host_name> ansible_ssh_host=<host_ip> ansible_ssh_user=<user_name_for_connect>

* Запускаем сценарий на исполнение: `ansible-playbook -i inventory/hosts playbook.yml --ask-pass --become --ask-become-pass --ask-vault-pass`

.. table:: 

==================== ==================================================================
Key                  INFO
==================== ==================================================================
-i                   Необходимо указать путь к файлу `inventory`
-v или -vv           Повышает информативность вывода, нужен для анализа ошибок
--become             Предоставляет повышение полномочий через `sudo` УЗ при подключение
--ask-pass           Запрашивает пароль УЗ под которой будет выполнен сценарий
--ask-become-pass    Запрашивает пароль УЗ при запуске `sudo`
--ask-vault-pass     Запрашивает пароль от файла с "секретами" 

.. note :: При запуске и в момент исполнения формируется файл с логами для анализа ошибок `logs/ansible-log.log`. Размер файла зависит от уровня подробного вызова и количества запусков сценария.
