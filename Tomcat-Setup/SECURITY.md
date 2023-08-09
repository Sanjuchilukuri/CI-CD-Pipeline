# Tomcat Security Guide

Ensuring the security of your Tomcat server is paramount. This guide offers recommendations and procedures to bolster the security of your Tomcat installation.

> ## Prerequisites
>
> - A configured Tomcat server. If not yet set up, refer to our [Tomcat Installation Guide](./INSTALL.md).

> ## Security Recommendations

> ### 1. Update Default Credentials
>
> The initial credentials packaged with Tomcat should always be changed, especially for the manager and admin interfaces.
>
> ```bash
> # Navigate to the conf directory
> cd path_to_tomcat/conf/
>
> # Open tomcat-users.xml
> vim tomcat-users.xml
> ```
> Alter the default users by introducing custom usernames and robust passwords.

> ### 2. Limit Access to Manager and Admin Apps
>
> Only recognized IPs should be granted access to the manager and admin user interfaces by employing IP whitelisting.
>
> ```bash
> # Navigate to the manager's META-INF directory
> cd path_to_tomcat/webapps/manager/META-INF/
>
> # Edit context.xml
> vim context.xml
> ```
> To restrict access, uncomment the Valve line.

```xml
<Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="127\.0\.0\.1"/>
> ### 3. Enable HTTPS
>
> When your Tomcat server is available online, always opt for HTTPS to encrypt traffic, necessitating the configuration of an SSL certificate.

> ### 4. Disable Unwanted Default Applications
>
> Tomcat is bundled with default apps which may be superfluous to your needs. It's prudent to disable or eliminate them.
>
> ```bash
> # Head to the webapps directory
> cd path_to_tomcat/webapps/
> # Remove unnecessary folders
> rm -rf examples/ docs/
> ```

> ### 5. Obscure Server Version Details
>
> ```bash
> # Open server.xml for editing
> vim path_to_tomcat/conf/server.xml
> ```
> In the `<Connector>` element, modify the `Server` attribute to a nondescript name or leave it blank.

> ### 6. Regularly Update Tomcat
>
> Continually check for Tomcat updates and implement them as necessary since they often contain vital security fixes.

> ### 7. Constrain HTTP Methods
>
> Only enable essential HTTP methods. If your application doesn't utilize the PUT or DELETE methods, it's advisable to deactivate them.

> ## Further Advice
>
> - Habitually scrutinize your Tomcat logs for any unusual activities.
> - For enhanced protection, think about setting up a Web Application Firewall (WAF) in front of Tomcat.
> - Establish a regular backup routine for your server and configurations.
> - Employ tools such as `jps` and `jstack` to monitor and dissect your JVM processes.

**Note**: Recognize that security is an ongoing endeavor. Stay updated with the latest vulnerabilities and best practices related to Tomcat and general web servers.
