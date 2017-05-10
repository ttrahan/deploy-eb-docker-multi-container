FROM tomcat:8

# Add files
RUN rm -rf /usr/local/tomcat/webapps/ROOT/*
COPY ./index.jsp /usr/local/tomcat/webapps/ROOT
EXPOSE 8080

# start container
ENTRYPOINT ["catalina.sh", "run"]




