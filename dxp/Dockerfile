# 
# The Liferay Portal 6.2 EE
#
# Build the image:
# docker build -t lfrdxp/dxp .
#
FROM lfrdxp/java-base
MAINTAINER Andre Fabbro <andre.fabbro@liferay.com>

ENV INSTALLDIR /opt
ENV LIFERAY_PACKAGE liferay-dxp-tomcat-7.1.10.1-sp1-20190110085705206.zip
ENV LIFERAY_PACKAGE_NAME_FOLDER liferay-dxp-7.1.10.1-sp1
ENV LIFERAY_LICENSE license.xml
ENV LIFERAY_FIXPACK liferay-fix-pack-dxp-6-7110.zip
ENV TOMCA_ROOT_CONF ROOT.xml

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

# Copy Tomcat Datasource Config
RUN rm -rf /opt/liferay/tomcat-9.0.6/conf/Catalina/localhost/$TOMCA_ROOT_CONF
COPY $TOMCA_ROOT_CONF /opt/liferay/tomcat-9.0.6/conf/Catalina/localhost/

# Install fix-pack
COPY $LIFERAY_FIXPACK /opt/liferay/patching-tool/patches/
RUN sh /opt/liferay/patching-tool/patching-tool.sh install

EXPOSE 8080 8009

# CMD ["bash"]
CMD ["/opt/liferay/tomcat-9.0.6/bin/catalina.sh", "run"]