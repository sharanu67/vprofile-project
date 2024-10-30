FROM openjdk:11 AS build

LABEL "Project"="Vprofile"
LABEL "Author"="Sharanu"

# Install maven
RUN apt-get update && apt-get install -y maven git

# Clone the repository and build the project
RUN git clone https://github.com/devopshydclub/vprofile-project
WORKDIR vprofile-project
RUN git checkout docker && mvn install

FROM tomcat:9-jre11

# Remove default Tomcat webapps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the built WAR file from the previous build stage
COPY --from=build /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Expose the port and start Tomcat
EXPOSE 8080
CMD ["catalina.sh", "run"]






# Wrong code of mine
#FROM openjdk:11 AS BUILD_IMAGE

#LABEL "Project"="Vprofile" 
#LABEL "Author"="Sharanu"

#RUN apt update && install maven -y
#RUN git clone https://github.com/devopshydclub/vprofile-project
#RUN cd vprofile-project && git checkout docker && maven install 

#FROM tomcat:9-jre11
#RUN rm -rf /usr/local/tomcat/webapps/*
#COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

#EXPOSE 8080
#CMD ["catalina.sh", "run"]
