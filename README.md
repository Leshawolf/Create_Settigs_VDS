# Подключение apache2,php,phpmyadmin,webmin для VDS
P.S. Небольшие комментарии обозначаю в данном разделе "///"

- `apt update`
- `apt list --upgradable`
- `apt upgrade` ##выбор 10
`reboot`  ///Для перезагрузки
`adduser <Имя пользователя>`
`usermod -aG sudo <Имя пользователя>`
`ufw app list` 

### Вывод:

> Available applications:OpenSSH 

`ufw allow OpenSSH`
`ufw enable`
`ufw status`

### Вывод:
>Status: active
>To               Action   From
>
>OpenSSH          ALLOW    Anywhere
>OpenSSH (v6)     ALLOW    Anywhere (v6)

# Переход на другого пользователя
`ssh <Имя пользователя>@<тут ваш ip>`
`sudo apt install apache2`
`sudo ufw app list`

### Вывод:
>Available applications:
>   Apache
>   Apache Full
>   Apache Secure
>   OpenSSH

`sudo ufw allow in "Apache Full"`
`sudo apt install mysql-server`
`sudo mysql_secure_installation`

### Вывод:
>Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG:
>
>/// 0-допускает поставить лёгкий пароль от 8 символов
>/// 1-допускает поставить пароль от 8 символов, с цифрами, с разными регистрами, с специальными знаками
>/// 2- допускает поставить пароль от 8 символов, с цифрами, с разными регистрами, с спецаильными знаками, с файлом словоря.

# ПРИ НЕОБХОДИМОСТИ СОЗДАНИЯ ПОЛЬЗОВАТЕЛЯ
### В случае получении ошибки:
>… Failed! Error: SET PASSWORD has no significance for user 'root'@'localhost'
>as the authentication method used doesn't store authentication data in the MySQL server.
>Please consider using ALTER USER instead if you want to change authentication parameters.

`sudo mysql`
`CREATE USER 'root'@'localhost' IDENTIFIED BY '11111111';` ///Создание нового пользователя Mysql
`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by '1111111';` ///Пароль должен подходить под выбраную защиту выше (LOW, MEDIUM, STRONG)
`sudo mysql_secure_installation`

# УСТАНОВКА PhpMyAdmin
`sudo apt -y install php-mbstring`
`sudo apt -y install phpmyadmin` ///Выбор Apache2
`sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf`
`sudo a2enconf phpmyadmin.conf`
`sudo systemctl restart apache2`
   
### НАСТРОЙКА WEBMIN
`sudo nano /etc/apt/sources.list`
`wget http://www.webmin.com/jcameron-key.asc`
`sudo apt-key add jcameron-key.asc`
`sudo apt-get update`
`sudo apt-get install webmin`
