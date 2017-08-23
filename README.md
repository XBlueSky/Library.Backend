# library.Backend  

## Description

This will show us how to install and configure `web server` [Apache-2.4](https://httpd.apache.org/download.cgi) . Also give some instructions that can be used to install the `framework`  [Flight](http://flightphp.com/) and `library` [php-activerecord](http://www.phpactiverecord.org/) we choose. 

Installs and configures web server [Apache-2.4](https://httpd.apache.org/download.cgi), database [mysql 5.7](https://dev.mysql.com/doc/relnotes/mysql/5.7/en/) by using oneinstack.And we choose [Flight](http://flightphp.com/), a fast, simple, extensible framework for PHP implementation with some additional features useful for us to quickly and easily build RESTful web applications.Also, we use [php-activerecord](http://www.phpactiverecord.org/)  which is an open source ORM library based on the ActiveRecord pattern to be more easily to handle SQL for common operations.

## Platform  
- CentOS 7 x64 

## Table of Contents    

- [Web server](#Web_server)  
- [Framework](#framework)  
- [Library](#library)  

## Web server  
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



