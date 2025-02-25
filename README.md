# OTUS PRO Homework 44 MySQL

## Домашняя работа 44: MySQL: Backup + Репликация

### Домашнее задание:
**1. Подготовка рабочего места**   
**2. В материалах приложены ссылки на вагрант для репликации и дамп базы bet.dmp**

Базу развернуть на мастере и настроить так, чтобы реплицировались таблицы:

| bookmaker   |   
| competition |   
| market      |   
| odds        |   
| outcome     |   
   
Настроить GTID репликацию   
 
---
## Выполнение задания:
### 1. Подготовка рабочего места:
Выполнение домашнего задания предполагает, что на компьютере установлен Vagrant+VirtualBox   
**[Как установить Vagrant на Debian 12](https://github.com/avlikh/Install_Vagrant_Debian12/blob/main/README.md)**   

Развернем Vagrant-стенд:
  - Создайте папку с проектом и зайдите в нее (например: /opt/otus/mysql):
```
mkdir -p /opt/otus/mysql ; cd /opt/otus/mysql
```
  - Клонируете проект с Github, набрав команду:
```
apt update -y && apt install git -y ; git clone https://github.com/avlikh/Otus_pro_44.git .
```
  - Запустите проект из папки, в которую склонировали проект (в нашем примере /opt/otus/mysql):
```
vagrant up
```
**Результатом выполнения команды vagrant up станет:** 
* созданные 2 виртуальных машины **mysqlsrs** и **mysqlrep** с установленными MySQL серверами;
* на MySQL source (mysqlsrs) загружен дамп таблицы 'bet';
* настроена GTID репликация с MySQL source (mysqlsrs) на MySQL replica (mysqlrep), при этом таблицы bet.events_on_demand и bet.v_same_event исключены из репликации.
---
### 2. В материалах приложены ссылки на вагрант для репликации и дамп базы bet.dmp**
Базу развернуть на мастере и настроить так, чтобы реплицировались таблицы:
| bookmaker   |   
| competition |   
| market      |   
| odds        |   
| outcome     |   
   
Настроить GTID репликацию   

Домашнее задание было выполнено при помощи Vagrant+Ansible.
   
Проверим что стенд коректно настроился и условия домашнего задания выполнены.


