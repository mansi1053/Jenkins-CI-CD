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




