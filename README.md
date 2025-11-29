# Домашнее задание к занятию «Система мониторинга Zabbix»
### Золоторев Н.Д.

### Задание 1

Установите Zabbix Server с веб-интерфейсом.
Процесс выполнения

    Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
    Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
    Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
    Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.

Требования к результатам

    Прикрепите в файл README.md скриншот авторизации в админке.
    Приложите в файл README.md текст использованных команд в GitHub.

### Решение 1

1. sudo apt update
2. sudo apt install postgersql
3. sudo wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb
4. sudo dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb
5. sudo apt update 
6. sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts
7. sudo -u postgres createuser --pwprompt zabbix
8. sudo -u postgres createdb -O zabbix zabbix 
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix 
9. sudo nano /etc/zabbix/zabbix_server.conf 
10. systemctl restart zabbix-server apache2
11. systemctl enable zabbix-server apache2 

<img src = "img/zabbix_web.png" width = 100%>

<img src = "img/zabbix_lk.png" width = 100%>



### Задание 2

Установите Zabbix Agent на два хоста.
Процесс выполнения

    Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
    Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
    Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
    Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
    Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

Требования к результатам

    Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
    Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
    Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
    Приложите в файл README.md текст использованных команд в GitHub

### Решение 2

1. sudo wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb
2. sudo dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb
3. sudo apt update
4. sudo apt install zabbix-agent
5. systemctl restart zabbix-agent
6. systemctl enable zabbix-agent 

<img src = "img/add_agents.png" width = 100%>

<img src = "img/latest_data1.png" width = 100%>

<img src = "img/latest_data2.png" width = 100%>

