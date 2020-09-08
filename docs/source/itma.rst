Установка агента мониторинга в ОС CentOS/RHEL с помощью Ansible
===============================================================
Роль для установки и настройки агента IBM Tivoli Monitoring (ITM)

список сервера TEMS для подключения агента:

.. csv-table:: 
   :header: "Регион", "Сервера"
   :widths: 15, 40

ГВЦ Собственно	для Linux серверо , gvc-rtems-01.gvc.oao.rzd
Москва                            , rtems-x86-msk.msk.oao.rzd
Санкт-Петербург	– ДЦУП            , orw-itmcup-01.orw.oao.rzd
Санкт-Петербург	– ПТК             , orw-itmapp-01.orw.oao.rzd
Санкт-Петербург	– СТО             , orw-itmsto-01.orw.oao.rzd
Санкт-Петербург	– ERP             , orw-itmsap-01.orw.oao.rzd
Калининград                       , orw-itmklg-01.orw.oao.rzd
Нижний Новгород                   , orw-itmnnw-01.orw.oao.rzd
Самара                            , orw-itmsam-01.orw.oao.rzd
Ярославль                         , orw-itmyar-01.orw.oao.rzd
Ростов                            , msk-rtems-ini-01.msk.oao.rzd; msk-rtems-ini-02.msk.oao.rzd
Саратов                           , msk-rtems-ini-01.msk.oao.rzd; msk-rtems-ini-02.msk.oao.rzd
Воронеж                           , msk-rtems-ini-01.msk.oao.rzd; msk-rtems-ini-02.msk.oao.rzd
Екатеринбург                      , svrw-tivoli-01.svrw.oao.rzd; svrw-tivoli-02.svrw.oao.rzd
Иркутск                           , svrw-tivoli-06.svrw.oao.rzd; svrw-tivoli-07.svrw.oao.rzd
Красноярск                        , svrw-tivoli-06.svrw.oao.rzd; svrw-tivoli-07.svrw.oao.rzd
Хабаровск                         , svrw-tivoli-06.svrw.oao.rzd; svrw-tivoli-07.svrw.oao.rzd
Новосибирск                       , svrw-tivoli-06.svrw.oao.rzd; svrw-tivoli-07.svrw.oao.rzd
Челябинск                         , svrw-tivoli-06.svrw.oao.rzd; svrw-tivoli-07.svrw.oao.rzd
Чита                              , svrw-tivoli-06.svrw.oao.rzd; svrw-tivoli-07.svrw.oao.rzd
Серверы СДО всех дорог            , svrw-tivoli-06.svrw.oao.rzd; svrw-tivoli-07.svrw.oao.rzd

.. note:: Для получения списка серверов необходимо обратиться в ЦК СМ.
