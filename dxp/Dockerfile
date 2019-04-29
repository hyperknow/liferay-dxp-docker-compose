# 
# The Liferay Portal 6.2 EE
#
# Build the image:
# docker build -t lfrdxp/dxp .
#
FROM nimmis/java-centos:oracle-8-jdk
MAINTAINER Andre Fabbro <andre.fabbro@liferay.com>

ENV INSTALLDIR /opt
ENV LIFERAY_PACKAGE liferay-dxp-digital-enterprise-7.0-sp6-fp39.zip
ENV LIFERAY_PACKAGE_NAME_FOLDER liferay-dxp-digital-enterprise-7.0-sp6
ENV LIFERAY_LICENSE license.xml
#ENV LIFERAY_FIXPACK liferay-fix-pack-dxp-6-7110.zip
ENV TOMCA_ROOT_CONF ROOT.xml
ENV SETENV setenv.sh

USER root

# Install additional packages
RUN yum update -y && yum -y install xmlstarlet saxon augeas bsdtar unzip telnet && yum clean all

WORKDIR $INSTALLDIR

COPY $LIFERAY_PACKAGE .

# Install Liferay Package
RUN unzip -q $LIFERAY_PACKAGE -d /opt \
	&& mv $LIFERAY_PACKAGE_NAME_FOLDER liferay \
	&& rm -rf $LIFERAY_PACKAGE

# Copy portal license
COPY $LIFERAY_LICENSE /opt/liferay/deploy/

# Copy portal ext properties
COPY portal-ext.properties /opt/liferay/

# Copy OSGi configs
COPY com.liferay.portal.store.file.system.configuration.AdvancedFileSystemStoreConfiguration.cfg /opt/liferay/osgi/configs/
COPY com.liferay.portal.search.elasticsearch6.configuration.ElasticsearchConfiguration.config /opt/liferay/osgi/configs/

# Copy Tomcat Datasource Config
RUN rm -rf /opt/liferay/tomcat-8.0.32/conf/Catalina/localhost/$TOMCA_ROOT_CONF
COPY $TOMCA_ROOT_CONF /opt/liferay/tomcat-8.0.32/conf/Catalina/localhost/

# Copy setenv.sh
RUN rm -f /opt/liferay/tomcat-8.0.32/bin/setenv.sh
COPY $SETENV /opt/liferay/tomcat-8.0.32/bin/

# Install fix-pack
#COPY $LIFERAY_FIXPACK /opt/liferay/patching-tool/patches/
#RUN sh /opt/liferay/patching-tool/patching-tool.sh install

EXPOSE 8009/tcp
EXPOSE 8080/tcp
EXPOSE 8000/tcp
EXPOSE 11311/tcp

# CMD ["bash"]
CMD ["/opt/liferay/tomcat-8.0.32/bin/catalina.sh", "run"]