There are two database images you can choose from, MySQL:5.7 or MariaDB. 
As the password authentication method changed in MySQL 8, if you really want to use MySQL, please choose version 5.7 or you need extra command^1 listed below.

I don’t bother with extra settings so I will stick with MariaDB.

- Volume:

I create named volume called wp-db-data[^2] here. We use named volume for persistent data. 
You won’t lost your data when you upgrade WordPress nor even remove the container.

- Network:

I add this database service to default network to avoid unrelated containers from accessing this container. 
Docker use the folder name as prefix when it creates default network. For example my docker-compose file is in ~/wordpressfolder, docker will create default network as wordpress_default.

- Environment

I set root password, database name, username and password here.

Please do NOT use such simple username/password in production environment

- Service : WordPress
depends_on: db
- WordPress will run after db. If we stop both containers, WordPress will be stopped before db.
Image:

I used the latest version of WordPress official image.
Environment

DB-HOST will be the port 3306 of db service. 
The other variables are just database name, username and password. 
		
- Volumes

I mount /var/www/html from WordPress container to our local folder ./wp-data. 
The benefit of doing that is we can modify files on our server directly. 
For example if we need to upload pictures, plugins or themes, we can put it in this folder straight away. In case your website is down due to bad plugin updates, you can also delete this plugin from here. There is no need to docker exec -it <mycontainer> bash any more.

- Label

This is the interesting part.

If a label defines a router (e.g. through a router Rule) and a label defines a service (e.g. implicitly through a loadbalancer server port value), but the router does not specify any service, then that service is automatically assigned to the router.

If a label defines a router (e.g. through a router Rule) but no service is defined, then a service is automatically created and assigned to the router.

In summary, if a user does not want to link router to a service, nor define any service labels. Traefik will take care of everything including creating service and assigning service to router (host name).

[^2]: Please note we must define this named container at the end of docker-compose file. I also named this volume wp-db-data, if we don’t use that, docker will add the folder name as prefix to your volume name. for example wordpress_db-data 
	

