# WordPress: in Docker with Docker-Compose:

- SOURCE: https://docs.docker.com/compose/wordpress/

- **Create docker containers:** <br />
Create "docker-compose.yml": nano docker-compose.yml: <br />
 <br />
 
```
    version: "3.9"
        
    services:
      db:
        image: mysql:5.7
        volumes:
          - db_data:/var/lib/mysql
        restart: always
        environment:
          MYSQL_ROOT_PASSWORD: somewordpress
          MYSQL_DATABASE: wordpress
          MYSQL_USER: wordpress
          MYSQL_PASSWORD: wordpress
        
      wordpress:
        depends_on:
          - db
        image: wordpress:latest
        ports:
          - "8000:80"
        restart: always
        environment:
          WORDPRESS_DB_HOST: db:3306
          WORDPRESS_DB_USER: wordpress
          WORDPRESS_DB_PASSWORD: wordpress
          WORDPRESS_DB_NAME: wordpress
    volumes:
      db_data: {}
	  
```

<br />

- **Build the project:** <br />
docker-compose up -d <br />

- **Test Wordpress:** <br />
- http://localhost:8000 <br />

- **Shutdown and cleanup** (removes the containers, default network, but preserves the WordPress database): <br />
docker-compose down <br />

- **Shutdown and cleanup** (removes the containers, default network, and the WordPress database): <br />
docker-compose down --volumes <br />
