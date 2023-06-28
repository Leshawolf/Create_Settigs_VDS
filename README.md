# Подключение apache2,php,phpmyadmin,webmin для VDS
P.S. Небольшие комментарии обозначаю в данном разделе "///"

1) apt update
2) apt list --upgradable
3) apt upgrade ##выбор 10
4) reboot  ///Для перезагрузки
5) adduser <Имя пользователя>
6) usermod -aG sudo <Имя пользователя>
7) ufw app list 

## Вывод

> Available applications:OpenSSH 

9) `ufw allow OpenSSH`
10) `ufw enable`
11) ufw status

## Вывод

\```
Status: active
To               Action   From
--               ------   ----
OpenSSH          ALLOW    Anywhere
OpenSSH (v6)     ALLOW    Anywhere (v6)
\```

# Переход на другого пользователя
1) ssh <Имя пользователя>@<тут ваш ip>
2) sudo apt install apache2
3) sudo ufw app list

## Вывод

\```
Available applications:
   Apache
   Apache Full
   Apache Secure
   OpenSSH
\```

5) sudo ufw allow in "Apache Full"
6) sudo apt install mysql-server
7) sudo mysql_secure_installation

## Вывод

\```
Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG:
/// 0-допускает поставить лёгкий пароль от 8 символов
/// 1-допускает поставить пароль от 8 символов, с цифрами, с разными регистрами, с специальными знаками
/// 2- допускает поставить пароль от 8 символов, с цифрами, с разными регистрами, с спецаильными знаками, с файлом словоря.
\```

# Если необходимо создать пользователя
## В случае получении ошибки:

## Ошибка

\```
… Failed! Error: SET PASSWORD has no significance for user 'root'@'localhost'
as the authentication method used doesn't store authentication data in the MySQL server.
Please consider using ALTER USER instead if you want to change authentication parameters.
\```

1) sudo mysql
2) CREATE USER 'root'@'localhost' IDENTIFIED BY '11111111'; ///Создание нового пользователя Mysql
3) ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by '1111111'; ///Пароль должен подходить под выбраную защиту выше (LOW, MEDIUM, STRONG)
4) sudo mysql_secure_installation

# Установка myadmin
1) sudo apt -y install php-mbstring
2) sudo apt -y install phpmyadmin ///Выбор Apache2
3) sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf
4) sudo a2enconf phpmyadmin.conf
5) sudo systemctl restart apache2
   
### НАСТРОЙКА WEBMIN
1) sudo nano /etc/apt/sources.list
2) wget http://www.webmin.com/jcameron-key.asc
3) sudo apt-key add jcameron-key.asc
4) sudo apt-get update
5) sudo apt-get install webmin
