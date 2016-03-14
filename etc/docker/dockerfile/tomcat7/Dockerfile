FROM localhost:5000/centos7-base:latest
MAINTAINER frefol 

######## JDK7

#Note that ADD uncompresses this tarball automatically
ENV JAVA_MAJOR 7
ENV JAVA_BUILD 72
ENV JAVA_VERSION 1.${JAVA_MAJOR}.0_${JAVA_BUILD}
ENV JAVA_HOME=/opt/jdk${JAVA_VERSION}
ENV JAVA_OPTS -Dsun.security.krb5.debug=true -Dsun.security.spnego.debug=true -Djava.security.krb5.conf=/etc/
ADD jdk-${JAVA_MAJOR}u${JAVA_BUILD}-linux-x64.tar.gz /opt
WORKDIR ${JAVA_HOME}

RUN alternatives --install /usr/bin/java java ${JAVA_HOME}/bin/java 1
RUN alternatives --install /usr/bin/jar jar ${JAVA_HOME}/bin/jar 1
RUN alternatives --install /usr/bin/javac javac ${JAVA_HOME}/bin/javac 1
RUN echo "JAVA_HOME=${JAVA_HOME}" >> /etc/environment

# Update Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files 7
# http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html
# This file is needed for SSO support
ADD local_policy.jar ${JAVA_HOME}/jre/lib/security/
ADD US_export_policy.jar ${JAVA_HOME}/jre/lib/security/
 
######## TOMCAT
 
#Note that ADD uncompresses this tarball automatically
ENV CATALINA_HOME /usr/share/tomcat
ENV PATH ${CATALINA_HOME}/bin:$PATH
ENV TOMCAT_MAJOR 7
ENV TOMCAT_VERSION 7.0.64

ADD apache-tomcat-${TOMCAT_VERSION}.tar.gz /usr/share
RUN mv /usr/share/apache-tomcat-${TOMCAT_VERSION} ${CATALINA_HOME}
RUN echo "JAVA_HOME=/opt/jdk1.7.0_72/" >> /etc/default/tomcat

# Add tomcat group and user
RUN groupadd tomcat
RUN useradd -s /bin/bash -g tomcat tomcat

WORKDIR $CATALINA_HOME
# Remove extranneous Tomcat files
RUN rm -fr webapps
RUN mkdir -p ${CATALINA_HOME}/webapps/ROOT

# Create a simple HTML page in root folder that redirects 
# traffic to the Managed Services page.
RUN echo '<!DOCTYPE html>' >> ${CATALINA_HOME}/webapps/ROOT/index.html
RUN echo '<html>' >> ${CATALINA_HOME}/webapps/ROOT/index.html
RUN echo '<head>' >> ${CATALINA_HOME}/webapps/ROOT/index.html
RUN echo '<meta http-equiv="Refresh" content="0; url=/ms/" />' >>  ${CATALINA_HOME}/webapps/ROOT/index.html
RUN echo '<title>Managed Services Home</title>' >>  ${CATALINA_HOME}/webapps/ROOT/index.html
RUN echo '<body>' >> ${CATALINA_HOME}/webapps/ROOT/index.html
RUN echo 'Welcome to Managed Services' >>  ${CATALINA_HOME}/webapps/ROOT/index.html
RUN echo '</body>' >> ${CATALINA_HOME}/webapps/ROOT/index.html
RUN echo '</html>' >> ${CATALINA_HOME}/webapps/ROOT/index.html

# Change owner to Tomcat user and group
RUN chown -Rf tomcat.tomcat ${CATALINA_HOME}

# Expose port 8080
EXPOSE 8080

# Start Tomcat
CMD ["/usr/bin/su","-","tomcat","/usr/share/tomcat/bin/catalina.sh","run"]

