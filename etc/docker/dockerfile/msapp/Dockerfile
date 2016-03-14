# Pull base image
FROM localhost:5000/tomcat7:latest
MAINTAINER frefol 

# Add war file
ADD ms.war  /usr/share/tomcat/webapps/

# Start Tomcat
#CMD ["/usr/bin/su","-","tomcat","/usr/share/tomcat/bin/catalina.sh","run"]
