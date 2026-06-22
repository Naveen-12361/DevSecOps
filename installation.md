# Docker installation
sudo apt install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
sudo usermod -aG docker $USER && newgrp docker
docker --version


# Docker-compose installation
sudo apt install docker-compose -y
docker-compose --version


# insatll java [Required for jenkins]
sudo apt install fontconfig openjdk-17-jre -y
java -version


# install jenkins
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
/usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
/etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins -y

sudo systemctl enable jenkins
sudo systemctl start jenkins


# SonarQube Server Installation
docker run -itd --name sonarqube -p 9000:9000 sonarqube:lts-community


# Trivy installation
sudo apt install wget apt-transport-https gnupg lsb-release -y
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] \
https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | \
sudo tee /etc/apt/sources.list.d/trivy.list
sudo apt update
sudo apt install trivy -y

# Commands
image scan -> trivy image nginx:latest
Trivy File System Scan:
      Scan current directory:
                          trivy fs .
      Scan a specific folder:
                          trivy fs /path/to/project 
                     Example:
                          trivy fs ./wanderlust

Show only HIGH and CRITICAL vulnerabilities:
                                     trivy image --severity HIGH,CRITICAL myapp:latest
                                     trivy fs --severity HIGH,CRITICAL .

Generate a report:
                  trivy image -f table -o trivy-report.txt myapp:latest
                  trivy fs -f table -o fs-report.txt .



#Required Plugins
1. SonarQube Scanner
2. Sonar Quality Gates
3. OWASP Dependency-Check
4. Docker





# jenkins -> Sonar [URL (via webhook) + Token(in sonar)

                  







