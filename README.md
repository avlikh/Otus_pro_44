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
### 2. Домашнее задание было выполнено при помощи Vagrant+Ansible.
   
Проверим что стенд коректно работает и условия домашнего задания выполнены.

Зайдем на мастер и повысим полномочия до root: 
```   
vagrant ssh mysqlsrs   
```
```
sudo -i
```

Зайдем в mysql:   
```
mysql
```
Выведим список баз данных:
```
show databases;
```
<details>
<summary> результат выполнения команды: </summary>

```
+--------------------+
| Database           |
+--------------------+
| bet                |
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.01 sec)
```
</details>

Выберим базу 'bet'
```
use bet;
```

Посмотрим таблицы базы данных:

```
show tables;
```
<details>
<summary> результат выполнения команды: </summary>

```
+------------------+
| Tables_in_bet    |
+------------------+
| bookmaker        |
| competition      |
| events_on_demand |
| market           |
| odds             |
| outcome          |
| v_same_event     |
+------------------+
7 rows in set (0.01 sec)
```
</details>



и посмотрим таблицы в базе данных 'bet'   
Для этого выполним 
```
id vagrant && id root && id otusadm && id otus
```
<details>
<summary> результат выполнения команды: </summary>

```
uid=1000(vagrant) gid=1000(vagrant) groups=1000(vagrant),1003(admin)
uid=0(root) gid=0(root) groups=0(root),1003(admin)
uid=1001(otusadm) gid=1001(otusadm) groups=1001(otusadm),1003(admin)
uid=1002(otus) gid=1002(otus) groups=1002(otus)
```
</details>
