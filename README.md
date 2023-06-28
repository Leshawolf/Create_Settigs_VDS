В данном разделе показано подключение apache2,php,phpmyadmin,webmin для VDS

## Начало
1) apt update
2) apt list --upgradable
3) apt upgrade ##выбор 10
4) reboot #Для перезагрузки
5) adduser <Имя пользователя>
6) usermod -aG sudo <Имя пользователя>
7) ufw app list 

##Вывод

![image](https://github.com/Leshawolf/Create_Settigs_VDS/assets/74571120/a9a3beda-0845-43a4-b685-f779d4ccc71f)

9) ufw allow OpenSSH
10) ufw enable
11) ufw status

##Вывод

![image](https://github.com/Leshawolf/Create_Settigs_VDS/assets/74571120/711d77ca-ca58-4fd6-9312-8d4d76753d64)

#Переход на другого пользователя
1) ssh <Имя пользователя>@<тут ваш ip>
2) sudo apt install apache2
3) sudo ufw app list

##Вывод

![image](https://github.com/Leshawolf/Create_Settigs_VDS/assets/74571120/d36ab10b-1fe6-49c5-8346-739d80d4e799)

5) sudo ufw allow in "Apache Full"
6) sudo apt install mysql-server
7) sudo mysql_secure_installation

##Вывод

![image](https://github.com/Leshawolf/Create_Settigs_VDS/assets/74571120/a730ede4-0d36-43f1-aaaf-d5ee116b80d8)

#Если необходимо создать пользователя
##В случае получении ошибки:##

##Ошибка

![image](https://github.com/Leshawolf/Create_Settigs_VDS/assets/74571120/3b00a810-f565-489e-938a-ffe8c26eaeb4)

1) sudo mysql
2) CREATE USER 'root'@'localhost' IDENTIFIED BY '11111111';#Создание нового пользователя Mysql
3) ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by '1111111';#Пароль должен подходить под выбраную защиту выше (LOW, MEDIUM, STRONG)
4) sudo mysql_secure_installation

#Установка myadmin
1) sudo apt -y install php-mbstring
2) sudo apt -y install phpmyadmin #Выбор Apache2
3) sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf
4) sudo a2enconf phpmyadmin.conf
5) sudo systemctl restart apache2
   
### НАСТРОЙКА WEBMIN
1) sudo nano /etc/apt/sources.list
2) wget http://www.webmin.com/jcameron-key.asc
3) sudo apt-key add jcameron-key.asc
4) sudo apt-get update
5) sudo apt-get install webmin
