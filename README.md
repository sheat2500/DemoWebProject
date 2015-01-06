# Docker Java/MySQL Tomcat Sample
This is a simple Java application that shows Java and MySQL.

# Run

## Fig
* `fig up -d`

Then run `fig ps` to find the app port.

## Standalone

* `docker run -d -P -e MYSQL_USER=java -e MYSQL_PASSWORD=java -e MYSQL_DATABASE=javatest MYSQL_ROOT_PASSWORD=java --name mysql mysql`
* `docker run -ti --rm --link mysql:mysql -v $(pwd):/host --entrypoint /bin/bash mysql -c "sleep 10; mysql -u java --password=java -h mysql javatest < /host/init.sql; exit 0"`
* `docker build -t javatest .`
* `docker run -ti -P --rm --link mysql:mysql javatest`

## Update Procedure

* `docker run --link=dockersamplejavamysqltomcat_db_1:mysql --entrypoint="mysql" -v $(pwd):/host mysql:5.6.21 -u java --password=java --host=mysql javatest < update.sql`
You should be able to access the app on http://<docker-host-ip>:<app-port>/dbtest
