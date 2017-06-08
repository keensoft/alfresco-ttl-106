FROM keensoft/alfresco-docker-template:201702-GA
MAINTAINER keensoft.es

RUN set -x \
	&& yum install -y \
	ImageMagick \
	ghostscript \
	&& yum clean all

ENV ALF_HOME /usr/local/alfresco
ENV CATALINA_HOME /usr/local/alfresco/tomcat
WORKDIR $ALF_HOME

# basic configuration
RUN set -x \
        && ln -s /usr/local/tomcat /usr/local/alfresco/tomcat \
	&& mkdir -p $CATALINA_HOME/conf/Catalina/localhost $CATALINA_HOME/shared/classes/alfresco/extension $CATALINA_HOME/shared/lib $ALF_HOME/modules/platform \
	&& mv $DIST/web-server/conf/Catalina/localhost/alfresco.xml tomcat/conf/Catalina/localhost/ \
        && mv $DIST/web-server/lib/*.jar tomcat/lib/ \
        && mv $DIST/web-server/webapps/alfresco.war tomcat/webapps/ \
        && mv $DIST/alf_data . \
        && mv $DIST/amps . \
        && mv $DIST/bin . \
        && mv $DIST/licenses . \
        && mv $DIST/README.txt . \
        && rm -rf $CATALINA_HOME/webapps/docs \
        && rm -rf $CATALINA_HOME/webapps/examples \
        && rm -rf $DIST 

COPY assets/tomcat/catalina.properties tomcat/conf/catalina.properties
COPY assets/tomcat/setenv.sh tomcat/bin/setenv.sh
COPY assets/alfresco/alfresco-global.properties tomcat/shared/classes/alfresco-global.properties

# Install Alfresco Office Services
RUN set -x \
        && mkdir /tmp/aos \
        && wget --no-check-certificate https://download.alfresco.com/release/community/201702-build-00016/alfresco-aos-module-1.1.5.zip \
        && unzip alfresco-aos-module-1.1.5.zip -d /tmp/aos \
        && mv /tmp/aos/extension/* tomcat/shared/classes/alfresco/extension \
        && mv /tmp/aos/alfresco-aos-module-1.1.5.amp amps \
        && mv /tmp/aos/aos-module-license.txt licenses \
        && mv /tmp/aos/_vti_bin.war tomcat/webapps \
        && rm -rf /tmp/aos alfresco-aos-module-1.1.5.zip

# Add api-explorer WAR file
RUN set -x \
	&& wget https://artifacts.alfresco.com/nexus/service/local/repositories/releases/content/org/alfresco/api-explorer/5.2.0/api-explorer-5.2.0.war -O tomcat/webapps/api-explorer.war

ENV PATH $ALF_HOME/bin:$PATH
ENV LANG es_ES.utf8

EXPOSE 8080 21 25 143 139 445
VOLUME $ALF_HOME/alf_data
CMD ["catalina.sh", "run"]