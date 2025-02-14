FROM ubuntu:latest
RUN apt-get update && apt install maven -y && apt install unzip -y && apt install wget -y
RUN wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.99/bin/apache-tomcat-9.0.99.zip
RUN unzip apache-tomcat-9.0.99.zip
COPY online-book-store/onlinebookstore_Source_code-master /mnt
WORKDIR /mnt
RUN mvn clean package
WORKDIR /apache-tomcat-9.0.99
RUN cp /mnt/target/onlinebookstore.war webapps
RUN chmod 777 bin/*
EXPOSE 8080
CMD ["/apache-tomcat-9.0.99/bin/catalina.sh", "run"]
