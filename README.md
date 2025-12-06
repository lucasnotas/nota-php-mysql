# nota-php-zorin



<h1>Comando instalação php 8.3 no zorin</h1>
<p>Adiciona repositorio</p>
	
	sudo add-apt-repository ppa:ondrej/php
</br>
<p>atualiza</p>

	sudo apt update
</br>
<p>upgrade</p>

	sudo apt upgrade
</br>
<p>Instal php 8.3</p>

	sudo apt install php8.3
</br>
<p>instalando pacotes adicionais</p>

	sudo apt-get install php8.3-nome_pacote_adicional
 </br>

  
<p>instalando pacotes mais comuns:</p>

	sudo apt-get install -y php8.3-cli php8.3-common php8.3-fpm php8.3-mysql php8.3-zip php8.3-gd php8.3-mbstring php8.3-curl php8.3-xml php8.3-bcmath
</br>
  
<p>Listar modulos instalados</p>

	php -m
 </br>
	
	
<p>configuraçoes:</p>

	/etc/php/8.3/apache2/php.ini
 </br>
 <h2>Instalando cliente mariaDB par mysql</h2>

	apt install mariadb-server mariadb-client -y
</br>
<p>Habilitando permições, Enter em todos definindo senha para root</p>

	mysql_secure_installation
</br>




<h2>Instalando PHPMYADMIN</h2>
<p>Entre na pasta para instalar o phpmyadmin</p>

	cd /usr/share
</br>
<p>Baixe o phpmyadmin</p>

	wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.zip -O phpmyadmin.zip
</br>
<p>Descompactar o arquivo</p>

	unzip phpmyadmin.zip
	
</br>
<p>Apague o arquivo baixado depois de descompactar</p>

	rm phpmyadmin.zip
	
</br>
<p>Renomeando pasta descompactada</P>

	mv phpMyAdmin-*-all-languages phpmyadmin
	
</br>
<p>Dando permição no arquivo</p>

	chmod -R 0755 phpmyadmin
	
</br>
<p>abara as o arquivo de configuração</p>

	nano /etc/apache2/conf-available/phpmyadmin.conf
	
</br>
<p>Adicione o seguinte conteudo</p>





Alias /phpmyadmin /usr/share/phpmyadmin

&lt;Directory /usr/share/phpmyadmin&gt;
    Options SymLinksIfOwnerMatch
    DirectoryIndex index.php
&lt;/Directory&gt;


&lt;Directory /usr/share/phpmyadmin/templates&gt;
    Require all denied
&lt;/Directory&gt;
&lt;Directory /usr/share/phpmyadmin/libraries&gt;
    Require all denied
&lt;/Directory&gt;
&lt;Directory /usr/share/phpmyadmin/setup/lib&gt;
    Require all denied
&lt;/Directory&gt;



	
</br>
<p>Reinicie o apache</p>

	systemctl reload apache2
	
</br>
<p>Crie uma pasta temporaria para o phpmyadmin</p>

	mkdir /usr/share/phpmyadmin/tmp/
	
</br>
<p>Atribuindo permições para a pasta temporaria</p>

	chown -R www-data:www-data /usr/share/phpmyadmin/tmp/
	
</br>
<p>Efetue login no terminla mysql</p>

	mysql -u root
	
</br>
<p>Execute as permições</p>

	UPDATE mysql.user SET plugin = 'mysql_native_password' WHERE user = 'root' AND plugin = 'unix_socket';
	
</br>
<p>Maximo de privilegios</p>

	FLUSH PRIVILEGES;
	
</br>
<p>So sair e testar</p>

	exit
	
</br>

<h2>Alternativa parainstalar o PHPMYADMIN</h2>
<p>execute o comando</p>

	sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl -y
</br>
<p>Selecione com ESPAÇO a opção apache2 e depois click em SIM e crie uma senha</p>
<p>Ative a extenção no php</p>

	sudo phpenmod mbstring
</br>
<p>Reinicie o apache</p>

	sudo systemctl restart apache2
</br>





<h2>Configurnado .htacss</h2>

	sudo a2enmod rewrite
	
</br>
<p>habilitando no arquivo de configuração</p>

	sudo nano /etc/apache2/apache2.conf
	
</br>
<p>Dentro da tag /var/www/ </p>

	AllowOverride All
	
</br>
<p>Reinicia apache </p>

	sudo service apache2 restart
	
</br>
<h1>PHP executa shell como admin</h1>
<h2>Remove a nececidade de informar senha pro usuario PHP</h2>
<p>Abra o arquivo sudoers</p>
	
	sudo nano /etc/sudoers
</br>
<p>Adicione no final da linha</p>

	apache ALL=(root)  NOPASSWD: /caminho/da/sua/pasta
</br>
<p>ou adicione o usuario</p>

	www-data ALL=NOPASSWD:ALL
</br>





<h1>Habilitar erro</h1>
<h2>Remove a nececidade de informar senha pro usuario PHP</h2>
<p>Abra o arquivo php.ini</p>
	
	sudo nano /etc/php/8.3/apache2/php.ini
</br>
<p>Altere os valores e encontre con Contr+w</p>

	display_errors = On
	display_startup_errors = On
	error_reporting = E_ALL
</br>
<p>Reicie o samba</p>

	sudo service apache2 restart
</br>

