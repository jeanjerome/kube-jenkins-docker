# Starting off with the Jenkins base Image
FROM jenkins/jenkins:lts
 
# Installing the plugins we need using the in-built install-plugins.sh script
RUN /usr/local/bin/install-plugins.sh git matrix-auth workflow-aggregator docker docker-workflow build-monitor-plugin credentials-binding

# Add jenkins to docker group to enable jenkins user to connect to docker socket
# switch to root, let the entrypoint drop back to jenkins
USER root
RUN groupadd -r docker \
 && usermod -aG docker jenkins
 
# Setting up environment variables for Jenkins admin user
ENV JENKINS_USER admin
ENV JENKINS_PASS admin
 
# Skip the initial setup wizard
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false
 
# Start-up scripts to set number of executors and creating the admin user
COPY executors.groovy /usr/share/jenkins/ref/init.groovy.d/
COPY default-user.groovy /usr/share/jenkins/ref/init.groovy.d/
 
VOLUME /var/jenkins_home
