# Use the official Ubuntu base image
FROM ubuntu:latest

# Set the working directory
WORKDIR /var/www/html/

# Update and upgrade
RUN apt-get update && apt-get upgrade -y

# Install Apache, PHP, MySQL support for PHP, and other dependencies
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y apache2 php libapache2-mod-php php-mysql curl nano

# Download and Extract WordPress using curl
RUN curl -O https://wordpress.org/latest.tar.gz && tar -xzvf latest.tar.gz && rm latest.tar.gz

# Giving permissions to the Apache user and group (www-data).
RUN chown -R www-data:www-data /var/www/html/wordpress


# Copy wp-config-sample.php and update database connection details
RUN cp /var/www/html/wordpress/wp-config-sample.php /var/www/html/wordpress/wp-config.php && \
    sed -i 's/database_name_here/my_db/' /var/www/html/wordpress/wp-config.php && \
    sed -i 's/username_here/farasat/' /var/www/html/wordpress/wp-config.php && \
    sed -i 's/password_here/123/' /var/www/html/wordpress/wp-config.php && \
    sed -i "s/localhost/db/" /var/www/html/wordpress/wp-config.php
# Update DB_HOST to match Docker Compose service name

#  Updates Apache settings, Configure Apache for WordPress
RUN echo "\
<VirtualHost *:80>\n\
    ServerAdmin webmaster@example.com\n\
    DocumentRoot /var/www/html/wordpress\n\
    ServerName localhost\n\
    <Directory /var/www/html/wordpress/>\n\
        AllowOverride All\n\
    </Directory>\n\
    ErrorLog \${APACHE_LOG_DIR}/error.log\n\
    CustomLog \${APACHE_LOG_DIR}/access.log combined\n\
</VirtualHost>" >/etc/apache2/sites-available/000-default.conf

# Enables the Apache rewrite module, which is often necessary for WordPress
RUN a2enmod rewrite

# Enable the virtual host and restart Apache
RUN a2ensite 000-default.conf && service apache2 restart

# Expose port 80
EXPOSE 80

# Start Apache in the foreground
CMD ["apache2ctl", "-D", "FOREGROUND"]
