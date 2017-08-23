# library.Backend  

## Description

This will show us how to install and configure `web server` [Apache-2.4](https://httpd.apache.org/download.cgi) . Also give some instructions that can be used to install the `framework`  [Flight](http://flightphp.com/) and `library` [php-activerecord](http://www.phpactiverecord.org/) we choose. 

Installs and configures web server [Apache-2.4](https://httpd.apache.org/download.cgi), database [mysql 5.7](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/) by using oneinstack.And we choose [Flight](http://flightphp.com/), a fast, simple, extensible framework for PHP implementation with some additional features useful for us to quickly and easily build RESTful web applications.Also, we use [php-activerecord](http://www.phpactiverecord.org/)  which is an open source ORM library based on the ActiveRecord pattern to be more easily to handle SQL for common operations.

## Platform  
- CentOS 7 x64 

## Table of Contents    

- [Web_server](#web_server)  
- [Framework](#framework)  
- [Library](#library)  
- [Other](#other)

## Web_server  
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




