#FROM localhost:5000/tomcat7:msapp
#FROM localhost:5000/jdk7:msapp
FROM localhost:5000/centos7-base:latest
MAINTAINER frefol 

RUN yum -y install httpd && yum clean all

# Start apache when container is started
# Simple startup script to avoid some issues observed with container restart 
ADD run-httpd.sh /usr/sbin/run-httpd.sh
RUN chmod -v +x /usr/sbin/run-httpd.sh

CMD ["/usr/sbin/run-httpd.sh"]
# Expose port 80
EXPOSE 80
 
