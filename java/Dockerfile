# 
# A Java base layer
#
# Build the image:
# docker build -t lfrdxp/java-base . 
#
FROM nimmis/java-centos:oracle-8-jdk
MAINTAINER Andre Fabbro <andre.fabbro@liferay.com>

USER root

# Install packages necessary to run EAP
RUN yum update -y && yum -y install xmlstarlet saxon augeas bsdtar unzip telnet && yum clean all
