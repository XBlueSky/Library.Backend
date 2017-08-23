# library.Backend  

## Description

This will show us how to install and configure `LAMP` [Apache-2.4](https://httpd.apache.org/download.cgi), database [mysql 5.7](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/) and [php 7.1](http://php.net/manual/en/migration71.php). Also give some instructions that can be used to install the `framework`  [Flight](http://flightphp.com/) and `library` [php-activerecord](http://www.phpactiverecord.org/) we choose. 

## Platform  
- CentOS 7 x64 

## Table of Contents    

- [LAMP](#lamp) 
- [Composer](#composer)
- [Framework](#framework)  
- [Library](#library)  
- [Other](#other)

## LAMP
we use `oneinstack` to be more easily to install Apache, MySQL, PHP.  

### Screen  installation
```ruby
  yum -y install wget screen
```
### Oneinstack installation  
```ruby
  wget http://mirrors.linuxeye.com/oneinstack-full.tar.gz  #download oneinstack
  tar xzf oneinstack-full.tar.gz                           #unzip
  cd oneinstack  
  screen -S oneinstack  
  sudo ./install.sh                                        #install 
```  

---  

```ruby
  upgrade operating system => n
  SSH port => 22
  install web server => y
  select Nginx server => 3                   #(do not install)
  select Apache server => 1                  #(Apache-2.4)
  select Tomcat server => 3                  #(do not install)
  install database => y
  version of database => 1                   #(mysql 5.7)
  password of database => oneinstack 
  select version of php => 5                 #(php 7.1)
  install opcode cache of php => y 
  select version of opcode cache of php => 1 #(Zend Opcode)
  install zendguardloader => n
  install ionCube => n
  install ImageMagick => n
  install Pure-FTPd => y
  install phpMyadmin => y
  install redis => y
  install memcached => y
  install HHVM => n
```  

---  

### configuration
#### modify `http.conf` path  

```ruby
  sudo vim /usr/local/apache/conf/httpd.conf
  ------------------------------------------
  DocumentRoot "/data/wwwroot/default"
  <Directory "/data/wwwroot/default">
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
  </Directory>
```  

#### modify `0.conf` path  

```ruby
  sudo vim /usr/local/apache/conf/vhost/0.conf
  --------------------------------------------
  <Directory "/data/wwwroot/default">
    SetOutputFilter DEFLATE
    Options FollowSymLinks ExecCGI
    Require all granted
    AllowOverride All
    Order allow,deny
    Allow from all
    DirectoryIndex index.html index.php
  </Directory>
```  

#### set `wwwroot` access privilege  

```ruby
  sudo chown -Rf nctulib /data/wwwroot/default/
```  
  
## Composer   
```ruby
  composer: cd /data/wwwroot/default/api                 #download composer
  sudo curl -sS https://getcomposer.org/installer | php
  cd /data/wwwroot/default/api                           #install
  chmod +x composer.phar
  sudo composer -v
  composer
  php composer-setup.php --version=1.0.0-alpha8
  php -r "unlink('composer-setup.php');"  
```  

## Framework
[Flight](http://flightphp.com/), a fast, simple, extensible framework for PHP implementation with some additional features useful for us to quickly and easily build RESTful web applications.  
  
```ruby  
  cd /data/wwwroot/default/api/vendor   #install
  composer require mikecao/flight  
```  

## Library  
[php-activerecord](http://www.phpactiverecord.org/)  which is an open source ORM library based on the ActiveRecord pattern to be more easily to handle SQL for common operations.  
  
```ruby  
  composer require php-activerecord/php-activerecord
```  

## Other  
#### modify `MySQL account/password` 

```ruby
  sudo vim /etc/ld.so.conf.d/mysql.conf
  sudo systemctl start mysqld
  sudo vim /data/wwwroot/default/phpMyAdmin/config.inc.php
```  

#### `URL` can be rewrite  
  
```ruby  
  sudo vim /usr/local/apache/conf/httpd.conf
  ------------------------------------------
  add LoadModule alias_module modules/mod_alias.so
  <Directory "/data/wwwroot/default">
  AllowOverride All
  </Directory>  
```  

#### Write `Rewrite Rule`  

```ruby  
  sudo vim /data/wwwroot/default/.htaccess
  <IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteBase /
    RewriteRule ^index\.html$ - [L]
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule . /index.html [L]
  </IfModule>
  sudo systemctl restart httpd
```  












