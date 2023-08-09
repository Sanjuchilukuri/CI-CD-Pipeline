# Jenkins Installation & Configuration Guide

This guide outlines the steps to install and configure Jenkins for our CI/CD pipeline.

> ## Prerequisites
>
> - A fresh instance (e.g., AWS EC2 instance).
> - User with `sudo` privileges.

> ## Installation Steps

> ### 1. Switch to the root user
>
> ```bash
> sudo -i
> ```

> ### 2. Update System Packages
>
> ```bash
> sudo yum update -y
> ```

> ### 3. Add Jenkins Repository
>
> Download the Jenkins repository:
>
> ```bash
> sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
> ```
>
> Import the Jenkins public key:
>
> ```bash
> sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
> ```

> ### 4. Install Jenkins & Java
>
> Install Open JDK 11:
>
> ```bash
> sudo amazon-linux-extras install java-openjdk11 -y
> ```
>
> Now, install Jenkins:
>
> ```bash
> yum install jenkins -y
> ```

> ### 5. Start Jenkins Service
>
> ```bash
> systemctl start jenkins
> ```

> ### 6. Initial Configuration
>
> Open a web browser and navigate to `http://your-server-ip:8080`. Follow the on-screen instructions to complete the initial setup.
>
> - Install the suggested plugins.
> - Create an admin user.
> - Configure the instance as required.

> ## Next Steps
>
> - Configuring build jobs.
> - Installing additional plugins.
> - Integrating with other tools in our CI/CD pipeline.

**Note**: Always refer to the official Jenkins documentation for any advanced configurations or troubleshooting.
