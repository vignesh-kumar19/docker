FROM viki19/centos-jre-python:0.8.27

#Set tomcat Versions as env variable
ENV TOMCAT_MAJOR_VER 7
ENV TOMCAT_FULL_VER 7.0.79

# installing MongoDB server
RUN yum install -y epel-release && yum install -y mongodb-server

# Installing tomcat 
RUN wget http://www.apache.org/dist/tomcat/tomcat-${TOMCAT_MAJOR_VER}/v${TOMCAT_FULL_VER}/bin/apache-tomcat-${TOMCAT_FULL_VER}.tar.gz && \
  tar xvzf apache-tomcat-${TOMCAT_FULL_VER}.tar.gz -C /opt/ && \
  rm -f apache-tomcat-${TOMCAT_FULL_VER}.tar.gz && \
  ln -s /opt/apache-tomcat-${TOMCAT_FULL_VER} /opt/tomcat && \
  rm -fr /opt/tomcat/webapps/examples /opt/tomcat/webapps/docs && \
  rm -rf /opt/tomcat/bin/*.bat && \
  mkdir -p /data/db

# Copying tomcat,mongoDB supervisor configuration file to startup service while running container
COPY conf/*.conf /etc/supervisor/conf.d/

#Creating Volume for MongoDB data directory
VOLUME /data/db/

EXPOSE 27017
EXPOSE 28017
EXPOSE 8080
