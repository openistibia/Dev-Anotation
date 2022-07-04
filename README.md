# Anotações de desenvolvimento
### Configurando o webserver
 ***[Linux - Ubuntu/Debian] Nginx + MySQL:***

 ## 1 - Instalação - Nginx:  
```
sudo apt update
sudo apt install nginx
sudo service nginx start

sudo ufw app list
sudo ufw allow in "Nginx Full"

Como testar: http://ip-do-servidor
```
## 2 - Instalação - MySQL:

```
sudo apt install mysql-server
sudo service mysql start
sudo mysql_secure_installation
```
<i>Este script irá perguntar se você deseja configurar o >> VALIDATE PASSWORD PLUGIN.

Atenção: ativar esta característica é uma decisão sua. 
Se habilitada, as senhas que não corresponderem ao critério especificado serão rejeitadas pelo MySQL com um erro. 
É seguro deixar a validação desativada, mas sempre utilize senhas fortes e únicas para as credenciais do banco de dados.

Responda Y para sim, ou qualquer outra coisa para continuar sem a habilitar.</i>

## 3 - Instalação - PHP:

```
sudo apt install php php-curl php-fpm php-mysql php-xml php-zip

sudo apt-get purge apache2*
sudo apt-get autoremove
cd /
cd etc
rm -r apache2
```
## 4 - Instalação - phpMyAdmin:

``sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl```

Depois você vera um tela.
Não selecionar nada.
Se você for solicitado a escolher um servidor da web, já que não há opção para Nginx, pressione  TAB e  ENTER 
para continuar sem selecionar um servidor da web.
Na proxima tela selecione YES para continuar.
Será solicitado a senha para o usuario root do seu phpmyadmin.

## 4.1 - Crie um link simbólico para o PHPMYADMIN
```sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin```

## 4.2 - Config necessário para phpMyAdmin funcionar com Nginx:

No terminal digite o seguinte comando:
```sudo apt install nano```
Depois de instalado vamos configurar o Nginx, então no terminal digite o seguinte comando:
```sudo nano /etc/nginx/sites-available/default```

Edite o objeto server o deixando desta maneira:

```
server {
	listen 80 default_server;
	listen [::]:80 default_server;

	root /var/www/html;

	# Add index.php to the list if you are using PHP
	index index.php  index.html index.htm index.nginx-debian.html;

	server_name _;

	location / {
		try_files $uri $uri/ =404;
	}

	location ~ \.php$ {
		include snippets/fastcgi-php.conf;
		fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
	}

	location ~ /\.ht {
		deny all;
	}
}
```
Reinicie o nginx
```sudo service nginx restart```<br>
## 4.3 - Config usuário mysql:

Se você tiver a autenticação por senha habilitada para o root user,você precisará executar o seguinte comando e digitar sua senha quando solicitada para poder se conectar:<br>
```sudo mysql -u root -p```<br>
A partir daí, crie um novo usuário e dê a ele uma senha forte:<br>
```CREATE USER 'seuuser'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'suasenha';```<br>
Nota: novamente, dependendo da versão do PHP que você instalou, aconselhamos definir seu novo usuário
para autenticar-se com o ```mysql_native_password``` em vez do ```caching_sha2_password```:<br>
```ALTER USER 'seuuser'@'localhost' IDENTIFIED WITH mysql_native_password BY 'suasenha';```
Então, conceda ao seu novo usuário os privilégios apropriados. <br>
Por exemplo, é possível conceder os privilégios de usuário para todas as tabelas dentro do banco de dados, além do poder de adicionar, alterar e remover os privilégios de usuário, com este comando:<br>
```GRANT ALL PRIVILEGES ON *.* TO 'seuuser'@'localhost' WITH GRANT OPTION;```<br>
Depois disso, saia do shell do MySQL:<br>
```exit```

