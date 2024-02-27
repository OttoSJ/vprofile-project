FROM openjdk:11 AS BUILD_IMGAE
RUN apt update && apt install maven -y 
RUN git clone https://github.com/OttoSJ/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install 

# Getting the base tomcat image form docker hub 
FROM tomcat:9-jre11

# This is removing the default webapp from the tomcat image so that it can be replaced in the next step below
RUN rm -rf /usr/local/tomcat/webapps/*

# This is coping the vprofile-v2.war artifact from the BUILD_IMAGE into the tomcat image at ROOT.war
COPY --from=BUILD_IMGAE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080

CMD ["catalina.sh", "run"]



