# Nexus Installation & Configuration Guide

This guide provides the steps to install and configure Sonatype Nexus 3 on Linux. The setup process is based on the guide from [devopscube](https://devopscube.com/how-to-install-latest-sonatype-nexus-3-on-linux/).

> ## Prerequisites
>
> - Root access to a Linux server.

> ## Installation Steps

> ### 1. Switch to the root user
>
> ```bash
> sudo -i
> ```

> ### 2. Install Java 1.8.0 OpenJDK
>
> ```bash
> yum install java-1.8.0-openjdk -y
> ```

> ### 3. Create a new directory
>
> ```bash
> mkdir /app
> ```

> ### 4. Navigate to the /app directory
>
> ```bash
> cd /app
> ```

> ### 5. Download Nexus
>
> ```bash
> sudo wget -O nexus.tar.gz https://download.sonatype.com/nexus/3/latest-unix.tar.gz
> ```

> ### 6. Unpack the downloaded file
>
> ```bash
> tar -zxvf nexus.tar.gz
> ```

> ### 7. Rename the extracted directory
>
> ```bash
> mv nexus-3.53.0-01 nexus
> ```

> ### 8. Create a new user for Nexus
>
> ```bash
> useradd nexus
> ```

> ### 9. Change directory ownership
>
> ```bash
> chown nexus:nexus nexus sonatype-work -R
> ```

> ### 10. Navigate to the Nexus directory
>
> ```bash
> cd nexus/
> ```

> ### 11. Navigate to the 'bin' directory
>
> ```bash
> cd bin/
> ```

> ### 12. Modify the `nexus.rc` file
>
> ```bash
> vim nexus.rc
> ```

> ### 13. Open and modify the `nexus.service` file
>
> ```bash
> vi /etc/systemd/system/nexus.service
> ```

> Insert the following configuration:

```ini
[Unit]
Description=nexus service
After=network.target

[Service]
Type=forking
LimitNOFILE=65536
User=nexus
Group=nexus
ExecStart=/app/nexus/bin/nexus start
ExecStop=/app/nexus/bin/nexus stop
Restart=on-abort

[Install]
WantedBy=multi-user.target
```
> ### 16. Add Nexus to Boot Services
> 
> ```bash
> chkconfig nexus on
> ```

> ### 17. Enable the `nexus.service`
> 
> ```bash
> systemctl enable nexus.service
> ```

> ### 18. Start Nexus
> 
> ```bash
> systemctl start nexus.service
> ```

> ### 19. Access Nexus on a Web Browser
> 
> Navigate to:
> 
> ```plaintext
> http:<public_ip>:8081
> ```

> ### 20. Sign Out and Then Sign In
> 
> Use `admin` as the username. For the password, retrieve it from the mentioned path in your Nexus setup and then set a new one.

**Note**: Always ensure to secure your Nexus setup with appropriate configurations and regular updates.
