Launch 2 EC2 instances (t2.medium)
  - Server
  - Agent

Allow inbount traffic on port 8080 for jenkins

Install the openjdk and jenkins package on EC2 instance
  -  sudo apt install openjdk-17-jre
  -  sudo apt-get install jenkins

Start jenins server
  - systemctl start jenkins
  - systemctl enable jenkins
  - systemctl status jenkins

Open browser and check jenkins accessible or not
  http://your-ec2-public-ip:8080 (replace your server machine public ip with (your-ec2-public-ip))

Retrieving Jenkins Initial Admin Password, execute the following command:
  - sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Use the password and unlock jenkins
Install suggested plugins
Setup the admin user
Setup the EC2 instance's private ip followed by :8080

Setup PostgreSQL doe SonarQube

Create a user and database for SonarQube

Install the SonnarQube
 - wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-25.7.0.110598.zip

Unzip the binaries:
  - unzip sonarqube-25.7.0.110598.zip

Move the file path to desired location:
  - sudo mv -v sonarqube-8.3.1.34397/* /opt/sonarqube

Create a group for sonar users:
  - sudo groupadd sonar

Add sonar user to EC2 user:
  - sudo usermod -a -G sonar ec2-user

Change the ownership of all the sonar files to the sonar user:
  - sudo chown -R sonar:sonar /opt/sonarqube

Change file access privileges:
  - sudo chmod -R 775 /opt/sonarqube

Set run as user:
  - sudo vi /opt/sonarqube/bin/linux-x86–64/sonar.sh
  - find the the line RUN_AS_USER=sonar, uncomment it

Modify the sonar.properties to add the details of postgreSQL:
  - sudo vi /opt/sonarqube/conf/sonar.properties

Add jdbc user name and password:
  - sonar.jdbc.username=sonar sonar.jdbc.password=sonar_passwor

Uncomment Postgres driver property.Remove current schema param if you are not using a custom schema for SonarQube database
  - sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube

Start the server:
  - /opt/sonarqube/bin/linux-x86–64/sonar.sh start

You can access the sonarQube UI at
  - http://<<EC2 instance public ip>>:9000/sonarqube
  (Allow inbount traffic on port 9000 for SonarQube)

Add plugins on jenkins
  - Git
  - Sonar:scanner

Push your application on Docker and use the docker image
Add your Docker Hub credentials in jenkins
