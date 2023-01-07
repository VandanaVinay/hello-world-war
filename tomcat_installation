#!/bin/bash
sudo apt-cache search tomcat
sudo apt install tomcat9 tomcat9-admin
sudo ufw allow from any to any port 9090 proto tcp
# changing the port number
sudo sed -i 's/port="8080"/port="9090"/g' /etc/tomcat9/server.xml
# including the configurations in users.xml file
sudo sh -c "echo '<role rolename=\"admin-gui\"/>' >> /etc/tomcat9/tomcat-users.xml"

sudo sh -c "echo '<role rolename=\"manager-gui\"/>' >> /etc/tomcat9/tomcat-users.xml"

sudo sh -c "echo '<user username=\"tomcat\" password=\"pass\" roles=\"admin-gui,manager-gui\"/>' >> /etc/tomcat9/tomcat-users.xml"

# Restarting the tomcat
sudo systemctl restart tomcat9
# giving passwordless access
sudo sh -c "echo 'jenkins ALL=(ALL) NOPASSWD: /var/lib/jenkins/workspace' >> /etc/sudoers"
sudo sh -c "echo 'jenkins ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers"
