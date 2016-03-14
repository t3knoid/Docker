FROM centos:7
MAINTAINER frefol 

#Helpful utils, but only sudo is required
RUN yum -y install sudo; yum clean all
RUN yum -y install net-tools; yum clean all
RUN yum -y install wget; yum clean all
RUN yum -y install unzip; yum clean all

ENV container docker
RUN yum -y update; yum clean all
