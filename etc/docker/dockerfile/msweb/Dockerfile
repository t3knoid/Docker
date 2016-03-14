# Pull base image
FROM localhost:5000/httpd2:latest
MAINTAINER frefol 

# Add web GUI files
ADD ms.zip  /var/www/html/

# Unzip website
WORKDIR /var/www/html
RUN unzip -q ms.zip
RUN rm -fr ms.zip
