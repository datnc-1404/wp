# working with local database
	# create database server, database. downloads mariadb-server
	sudo apt-get install mariadb-server
	# check mariadb-server
	systemctl status mariadb
[![z3210836286313-3cce03717894111c1f1449f0656176b5.jpg](https://i.postimg.cc/1tjMsTd3/z3210836286313-3cce03717894111c1f1449f0656176b5.jpg)](https://postimg.cc/JDjjQTmf)
	
	#connect local database and create database wp
	mysql -h localhost -u root
[![z3210841552458-acf6b4f6056b46f2c776fb8f6a39d88d.png](https://i.postimg.cc/HW38cXWb/z3210841552458-acf6b4f6056b46f2c776fb8f6a39d88d.png)](https://postimg.cc/z3bG4Lgf)

	#create database wp for wordpress
	create databse wp;
	#check database wp
	show databases;
[![z3210847261974-ec98d29ad4cb1bfeea4c6f1f6d465d83.jpg](https://i.postimg.cc/pLrSbfrC/z3210847261974-ec98d29ad4cb1bfeea4c6f1f6d465d83.jpg)](https://postimg.cc/LJdDjZzg)	
	
	#create user to use databse name wp
	MariaDB [(none)]> GRANT ALL PRIVILEGES ON wp.* TO 'amdin'@'localhost' IDENTIFIED BY '123456';
	MariaDB [(none)]> FLUSH PRIVILEGES;
	MariaDB [(none)]> EXIT
# working with Machine Ubuntu Server 20.4
	# open port 80; 22 
	sudo -i
	# install nginx
		apt update
		apt install nginx
	# install php
		add-apt-repository ppa:ondrej/php
		apt install php7.4-fpm php7.4-curl php7.4-mysql php7.4-xml 
	#check version php
[![z3210857826091-0f85b736e4c42e0a583b2d6aa9a57950.png](https://i.postimg.cc/cCVBpnb9/z3210857826091-0f85b736e4c42e0a583b2d6aa9a57950.png)](https://postimg.cc/PvQDZPhY)
	
	# install wordpress
		cd /var/www/
		curl -O https://wordpress.org/latest.tar.gz
		tar xzvf latest.tar.gz
		cd wordpress
		cp wp-config-sample.php wp-config.php
		nano wp-config.php
			# edit db_name, db_user, db_password, db_host  
[![z3210869089328-357f8ba6294a19b3c2d1d2477728b6fa.jpg](https://i.postimg.cc/3NmWS05F/z3210869089328-357f8ba6294a19b3c2d1d2477728b6fa.jpg)](https://postimg.cc/dZQqD10h)
			
			# add define('FS_METHOD','direct'); at the bottom
[![z3210872123606-98d9df24df682c6c058db96e04c0d1e7.png](https://i.postimg.cc/85hVxRcc/z3210872123606-98d9df24df682c6c058db96e04c0d1e7.png)](https://postimg.cc/KkvVMgnh)

		chmod -R 777 ./*
[![z3210864441120-1b4ebb42797ae696677c109337274102.png](https://i.postimg.cc/85X2rZ77/z3210864441120-1b4ebb42797ae696677c109337274102.png)](https://postimg.cc/Hc5Zq44m)
		
		#change file config nginx
		cd /etc/nginx/sites-enabled/
		nano default
			# exchange these statements:
				1: root /var/www/html;
				2: index index.html index.htm index.nginx-debian.html;
				3: server_name _;
			# to these statements:
				1: root /var/www/wordpress;
				2: index index.html index.htm index.php;
				3: server_name 0.0.0.0;
			# remove # before these statements
				1: location ~ \.php${
				2: include snippets/fastcgi-php.conf;
				3: fastcgi_pass unix:/var/run/php7.4-fpm.sock;
				4: }
[![z3210878262349-d0efd89395bfeaa2c00b2063e5280f34.jpg](https://i.postimg.cc/LXqTxS93/z3210878262349-d0efd89395bfeaa2c00b2063e5280f34.jpg)](https://postimg.cc/7Gk0LpT5)
		
		service nginx restart
# finish
[![z3210814459128-dd35a54707dfbb666a8e6c0d404444c8.jpg](https://i.postimg.cc/jSV68Rzc/z3210814459128-dd35a54707dfbb666a8e6c0d404444c8.jpg)](https://postimg.cc/fJK0ynqS)
# view private IP address
			# curl -4 icanhazip.com
# how to watch database?
		# apt install mysql-server
		# mysql -h <endpoint> -u admin -P 3306 -p
# install openssl
	#create ssl crt
	openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout privatekey.key -out certificate.crt
[![z3210900011359-58ee081d8d9860c8e301c5ba49020bed.jpg](https://i.postimg.cc/J7TWvc56/z3210900011359-58ee081d8d9860c8e301c5ba49020bed.jpg)](https://postimg.cc/K4gVgTVB)
	
	#change file default of nginx
[![z3210923448207-7bae79ab2c42d3a03f940263de3bfbd2.png](https://i.postimg.cc/tCZvChF4/z3210923448207-7bae79ab2c42d3a03f940263de3bfbd2.png)](https://postimg.cc/ZCmxwvfG)
	
	#test file nginx conf
	nginx -t
[![z3210928802754-0e506cc1c08fe614d1d6ea8b42d2701c.png](https://i.postimg.cc/9Q2k8DqX/z3210928802754-0e506cc1c08fe614d1d6ea8b42d2701c.png)](https://postimg.cc/D8C5mygR)
	
	#check page with port 443
[![z3210932687469-ec26c0b21385fe0dd5341e614c99f335.jpg](https://i.postimg.cc/43qb00Fv/z3210932687469-ec26c0b21385fe0dd5341e614c99f335.jpg)](https://postimg.cc/VS9CrKw5)

	#check page with port 80
[![z3210934507160-a017092be0ec0c8f87700526b7d778ec.jpg](https://i.postimg.cc/nzKj1w8h/z3210934507160-a017092be0ec0c8f87700526b7d778ec.jpg)](https://postimg.cc/ZBR5bHKG)
