MySQL
===================

Notes
-------------
>**MySQL Location** (*default* location on *Mac*)
>`/usr/local/mysql/bin`
>
>**Add MySQL to your PATH**
>*Add it to your PATH for the Current Session*
>`export PATH=${PATH}:/usr/local/mysql/bin`
>
>*Add it to your PATH Permanently*
>`echo 'export PATH="/usr/local/mysql/bin:$PATH"' >> ~/.bash_profile`
>
>To confirm, open a new *terminal* and run the command `mysql --version`.
>The output should be the following:
>```
>$ mysql --version
>mysql  Ver 8.0.16 for macos10.14 on x86_64 (MySQL Community Server - GPL)
>```
>
>**MySQL Service** (*on Mac*)
>Run the following command to **start**/**stop** the *MySQL service*.
>```
>sudo /usr/local/mysql/support-files/mysql.server start
>sudo /usr/local/mysql/support-files/mysql.server stop
>```
>
>**MySQL Service** (*on Ubuntu 18.04 LTS*)
>`systemctl status mysql.service`
>
>**MySQL Workbench**
>NOTE: *Remember to log out as the mysql user from the terminal before creating a MySQL Workbench connection*.
>

COMMANDS
-------------
>**Create a user**
>*syntax*
>`CREATE USER '<USER_NAME>'@'<HOST>' IDENTIFIED BY '<PASSWORD>'`
>*example*
>`CREATE USER 'joe1996'@'localhost' IDENTIFIED BY 'examplePa$$w0rd'`
>
>**Display user and host**
>*syntax*
>`SELECT user, host FROM mysql.user;`
>

Helpful Links
-------------
>[Official MySQL site](https://dev.mysql.com/)
>[MySQL Workbench](https://dev.mysql.com/downloads/workbench/)
>[Helpful Article on how to install and configure MySQL on ubuntu 18.04](https://vitux.com/how-to-install-and-configure-mysql-in-ubuntu-18-04-lts/)
>[Good reference for installing MySQL Workbench on ubuntu](https://ubuntu-mate.community/t/how-to-install-mysql-server-and-mysql-workbench-on-ubuntu-mate-18-04/17884)
