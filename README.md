#docker-joomla

This is a base Docker image that installs [Joomla](http://www.joomla.org/) - a popular open source content management system.

## Components
The stack comprises the following components (some are obtained through [dell/lamp-base](https://github.com/dell-cloud-marketplace/docker-lamp-base)):

Name       | Version                 | Description
-----------|-------------------------|------------------------------
Joomla	    | 3.3.6                   | Content Management System
Ubuntu     | see [docker-lamp-base](https://github.com/dell-cloud-marketplace/docker-lamp-base) | Operating system
MySQL      | see [docker-lamp-base](https://github.com/dell-cloud-marketplace/docker-lamp-base) | Database
Apache     | see [docker-lamp-base](https://github.com/dell-cloud-marketplace/docker-lamp-base) | Web server
PHP        | see [docker-lamp-base](https://github.com/dell-cloud-marketplace/docker-lamp-base) | Scripting language

## Usage

### Start the Container
Start the container, as follows:


    sudo docker run -d -p 80:80 -p 443:443 -p 3306:3306 --name joomla dell/joomla


### Advance Usage

Start your container with:

* Ports 80, 443 (Apache Web Server) and 3306 (MySQL) exposed
* A named container (**joomla**)
* A predefined password for the MySQL **admin** user
* A predefined hostname for the joomla container.
* Two data volumes (which will survive a restart or recreation of the container). The MySQL data is available in **/data/mysql** on the host. The PHP application files are available in **/app** on the host.

```no-highlight
sudo docker run -d \
    -p 80:80 \
    -p 443:443 \
    -p 3306:3306 \
    -v /app:/var/www/html \
    -v /data/mysql:/var/lib/mysql \
    -e MYSQL_PASS="password"  \
    --name joomla \
    dell/joomla
```


### Check the Log Files

If you haven't defined a MySQL password, the container will generate a random one. Check the logs for the password by running: 

     sudo docker logs joomla
     
You will see output like the following:

```no-highlight
====================================================================
You can now connect to this MySQL Server using:

   mysql admin -u admin -pca1w7dUhnIgI --host <host>  -h<host> -P<port>

   Please remember to change the above password as soon as possible!
   MySQL user 'root' has no password but only allows local connections
=====================================================================


========================================================================

   MySQL user: joomla and password: Me2rae1jiefi

========================================================================
```

Make a secure note of the passwords added to the users. You can use it later, to connect to MySQL (e.g. to backup data):

* The admin user password (in this case **ca1w7dUhnIgI**)
* The joomla user password (in this case **Me2rae1jiefi**)

Next, test the **admin** user connection to MySQL:

```no-highlight
mysql -uadmin -pca1w7dUhnIgI -h127.0.0.1 -P3306
```     


In this case, **ca1w7dUhnIgI** is the password allocated to the admin user. Make a secure note of this value. You can use it later, to connect to MySQL (e.g. to backup data):

    mysql -u admin -pca1w7dUhnIgI -h127.0.0.1 -P3306


## Complete the Installation

Open a web browser and navigate to either the public DNS or IP address of your instance. For example, if the IP address is 54.75.168.125, do:

    https://54.75.168.125

Your browser will warn you that the certificate is not trusted. If you are unclear about how to proceed, please consult your browser's documentation on how to accept the certificate.

You should see Joomla configuration wizard set to the ```Configuration``` tab, select your language and supply the requested information for the following fields:

* Site Name
* Admin Email
* Admin Username
* Admin Password
* Site Offline

Click on "Next" to proceed to the next step which will take you to the ```Database Configuration``` tab. And supply the MySQL information:

* Database Type: **MySQL**
* Hostname: **localhost**
* Username: **joomla**
* Password: *The joomla password read from the logs.*
* Database Name: **joomla**

Click on "Next" to proceed to the next step which will take you to the ```Overview" tab```. Select your preferred sample data and review the configuration set. Once reviewed you can complete the configuration by clicking on �Install�. On completion of installation you are requested to remove the installation folder by clicking �Remove installation folder�, this is a security feature and without this you are not able to proceed further.

Next click on �Site� or �Administrator� to redirect you to the newly created Joomla content management system.


### Getting Started

To start customising  Joomla, below are a few URLs as a starting guide:

* [Joomla Documentation](http://docs.joomla.org/Main_Page)
* [Getting Started with Joomla](http://docs.joomla.org/Getting_Started_with_Joomla!)
* [Joomla Extensions Directory](http://extensions.joomla.org/)
* [Joomla API](http://api.joomla.org/)


### Image Details

Pre-built Image   | [https://registry.hub.docker.com/u/dell/joomla](https://registry.hub.docker.com/u/dell/joomla)