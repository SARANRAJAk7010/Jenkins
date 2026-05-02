###Jenkins Installation and Setup**

1.  **Install Java (OpenJDK 17):**
    ```bash
    sudo apt install openjdk-17-jdk -y
    ```

2.  **Add Jenkins Repository and Install:**
    ```bash
    curl -fsSL [https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key](https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key) | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] [https://pkg.jenkins.io/debian-stable](https://pkg.jenkins.io/debian-stable) binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt update
    sudo apt install jenkins -y
    ```
    Remove Jenkins if needed
    ```bash
    sudo systemctl stop jenkins
    sudo apt remove jenkins -y
    sudo rm -rf /var/lib/jenkins
    ```
    or Try this installation
    ```bash
    wget https://pkg.jenkins.io/debian-stable/binary/jenkins_2.492.1_all.deb
    sudo dpkg -i jenkins_2.492.1_all.deb
    sudo apt --fix-broken install -y
    ```

4.  **Start and Enable Jenkins Service:**
    ```bash
    sudo systemctl start jenkins
    sudo systemctl enable jenkins
    ```

5.  **Initial Jenkins Setup:**
    * Retrieve the initial admin password:
        ```bash
        sudo cat /var/lib/jenkins/secrets/initialAdminPassword
        ```
    * Access the Jenkins dashboard at `http://<ec2-public-ip>:8080`.
    * Paste the password, install suggested plugins, and create an admin user.

6. **Add Sonarqube Repository and Install:**
    ```bash
    sudo apt update && sudo apt install unzip -y
    sudo adduser sonarqube
    sonarqube-10.4.1.88267.zip
    sudo mv sonarqube-10.4.1.88267 /opt/sonarqube
    sudo chown -R sonarqube:sonarqube /opt/sonarqube
    sudo su - sonarqube
    /opt/sonarqube/bin/linux-x86-64/sonar.sh start
    ```

