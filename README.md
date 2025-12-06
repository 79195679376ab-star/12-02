# Домашнее задание к занятию "`Работа с данными (DDL/DML)`" - `Абрамов Александр`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

### 1.1 Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.
<img width="791" height="146" alt="image" src="https://github.com/user-attachments/assets/2e56414e-6690-4e5c-9d44-a1e6e2cc99f2" />

### 1.2. Создайте учётную запись sys_temp.
<img width="950" height="294" alt="image" src="https://github.com/user-attachments/assets/060310c6-466d-45d1-8952-a79644e47129" />

### 1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)
<img width="690" height="298" alt="image" src="https://github.com/user-attachments/assets/c8dcaf6a-20aa-4704-99c1-5fb6d3d0fc7a" />
### 1.4. Дайте все права для пользователя sys_temp.
<img width="1101" height="130" alt="image" src="https://github.com/user-attachments/assets/f01eaa4e-40a4-430a-ba42-246abc0fedd3" />
### 1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/45ff8142-7810-453d-8d2d-f4b360acf950" />
### 1.6. Переподключитесь к базе данных от имени sys_temp.
### 1.7. Восстановите дамп в базу данных.
### 1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)
<img width="398" height="774" alt="image" src="https://github.com/user-attachments/assets/8328aa69-da2d-457a-ba00-192f7a1fe60e" />
### Простыня с запросами

# 1. Запуск контейнера
docker rm -f mysql8
docker run --name mysql8 -e MYSQL_ROOT_PASSWORD=rootpass -p 3307:3306 -d mysql:8.0
docker ps

# 2. Подключение как root
mysql -h 127.0.0.1 -P 3307 -u root -p

# 3. Создание пользователя
CREATE USER 'sys_temp'@'localhost' IDENTIFIED BY 'alexandr';

# 4. Список пользователей
SELECT user, host FROM mysql.user;

# 5. Права для sys_temp
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;

# 6. Список прав
SHOW GRANTS FOR 'sys_temp'@'localhost';

# 7. Переподключение
\q
mysql -h 127.0.0.1 -P 3307 -u sys_temp -p
SELECT CURRENT_USER();

# 8. Смена аутентификации (опционально)
ALTER USER 'sys_temp'@'localhost' IDENTIFIED WITH mysql_native_password BY '12345678';
FLUSH PRIVILEGES;

# 9. Загрузка дампа
wget https://downloads.mysql.com/docs/sakila-db.zip
unzip sakila-db.zip
mysql -h 127.0.0.1 -P 3307 -u root -p -e "CREATE DATABASE sakila;"
mysql -h 127.0.0.1 -P 3307 -u root -p sakila < sakila-schema.sql
mysql -h 127.0.0.1 -P 3307 -u root -p sakila < sakila-data.sql

# 10. Проверка таблиц
USE sakila;
SHOW TABLES;


### Задание 2 Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)

Название таблицы | Название первичного ключа
customer         | customer_id

<img width="1916" height="1060" alt="image" src="https://github.com/user-attachments/assets/6ed3a9c3-6c50-4481-800d-2c2f2baf5e42" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b37bc184-71e5-4383-8798-35766418de05" />
<img width="530" height="447" alt="image" src="https://github.com/user-attachments/assets/8dd1a607-9fae-4d8f-8177-dc9b87136577" />


