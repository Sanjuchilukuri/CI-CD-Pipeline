# TOMCAT Installation in Production

This guide covers the steps to install and configure Tomcat in a production environment.

> ## Prerequisites
>
> - Ensure you are logged into your Tomcat instance.
> - A fresh server instance (e.g., AWS EC2 instance).
> - User with `sudo` privileges.

> ## Installation Steps

> ### 1. Switch to the root user
>
> ```bash
> sudo -i
> ```

> ### 2. Navigate to the `/opt` Directory
>
> ```bash
> cd /opt
> ```

> ### 3. Download Tomcat
>
> Fetch the required version of Tomcat using:
>
> ```bash
> wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.78/bin/apache-tomcat-9.0.78.tar.gz
> ```

> ### 4. Unpack the Downloaded File
>
> To extract the files, use:
>
> ```bash
> tar -zxvf apache-tomcat-9.0.78.tar.gz
> ```

> ### 5. Modify `context.xml`
>
> Navigate to the manager's META-INF directory and open the `context.xml` for modification:
>
> ```bash
> cd apache-tomcat-9.0.78/webapps/manager/META-INF/
> vim context.xml
> ```
> Within Vim, use the command below to remove lines 21 and 22:
>
> ```bash
> 2dd
> ```

> ### 6. Navigate to `conf` Directory
>
> ```bash
> cd ../..
> cd conf/
> ```

> ### 7. Modify `tomcat-user.xml`
>
> Open the `tomcat-user.xml` file and incorporate the necessary users:
>
> ```bash
> vi tomcat-user.xml
> ```

> ### 8. Install Open JDK 11
>
> Install the necessary JDK using:
>
> ```bash
> amazon-linux-extras install java-openjdk11 -y
> ```

> ### 9. Start Tomcat
>
> Shift to the `bin` directory and initiate Tomcat:
>
> ```bash
> cd ../bin/
> sh startup.sh
> ```

> ### 10. Access Tomcat on a Web Browser
>
> To access the Tomcat server, open a web browser and input:
>
> ```
> http:<public_ip>:8080
> ```
> Subsequently, select "Manager App" and use the credentials configured in the previous steps to log in.

**Note**: The above steps will ensure your Tomcat server is installed and operational in the production environment.
