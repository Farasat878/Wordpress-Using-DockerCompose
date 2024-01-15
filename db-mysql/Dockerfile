# db-mysql/Dockerfile
FROM mysql:5.7


# Environment variables will be the MySQL server when it starts up.
# Name of initial db, pwd and user created when image is first started.
ENV MYSQL_ROOT_PASSWORD=123
ENV MYSQL_DATABASE=my_db
ENV MYSQL_USER=farasat
ENV MYSQL_PASSWORD=123

# Copy the database initialization script 
# SQL scripts (with a .sql extension) placed in this directory will be automatically executed when the MySQL container is started for the first time
COPY ./init.sql /docker-entrypoint-initdb.d/


# Expose MySQL port
EXPOSE 3306

