# SonarQube Setup Guide

This guide provides detailed steps on setting up SonarQube, a platform used for continuous inspection of code quality.

> ## Prerequisites
>
> Before starting the installation process, ensure you have root access on your server.

> ## Installation Steps

> ### 1. Switch to the Root User
>
> ```bash
> sudo -i
> ```

> ### 2. Navigate to `/opt` Directory
>
> ```bash
> cd /opt
> ```

> ### 3. Download SonarQube
>
> ```bash
> wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-8.9.6.50800.zip
> ```

> ### 4. Unzip the Downloaded File
>
> ```bash
> unzip sonarqube-8.9.6.50800.zip
> ```

> ### 5. Install Open JDK 11
>
> ```bash
> amazon-linux-extras install java-open-jdk11 -y
> ```

> ### 6. Create a New User for SonarQube
>
> ```bash
> useradd sonar
> ```

> ### 7. Update Ownership of SonarQube Directory
>
> ```bash
> chown sonar:sonar sonarqube-8.9.6.50800 -R
> ```

> ### 8. Modify Permissions of the SonarQube Directory
>
> ```bash
> chmod 777 sonarqube-8.9.6.50800 -R
> ```

> ### 9. Switch to 'sonar' User
>
> ```bash
> su – sonar
> ```

> ### 10. Navigate to the SonarQube Directory
>
> ```bash
> cd /opt/sonarqube-8.9.6.50800
> ```

> ### 11. Go to the 'bin' Directory
>
> ```bash
> cd bin/
> ```

> ### 12. Access the 'linux' Sub-directory
>
> ```bash
> cd linux-x86-64/
> ```

> ### 13. Start the SonarQube Service
>
> ```bash
> sh sonar.sh start
> ```

> ### 14. Check SonarQube Service Status
>
> ```bash
> sh sonar.sh status
> ```

> ### 15. Access SonarQube from a Web Browser
>
> Open your preferred web browser and navigate to:
> 
> ```plaintext
> http://<public_ip>:9000
> ```

> ### 16. Login to SonarQube
>
> Use 'admin' as both username and password for the initial login.

> ### 17. Reset the Default Password
>
> After the initial login, you will be prompted to set a new password for the 'admin' user.

**Note**: Always refer to the official SonarQube documentation for additional configurations or any troubleshooting steps.

