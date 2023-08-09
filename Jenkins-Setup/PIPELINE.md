# SONAR Setup

## Prerequisites
Before starting the setup, ensure you have the necessary permissions and credentials.

## Setup Instructions

> ### 1. Switch to Root User
>
> ```bash
> sudo -i
> ```

> ### 2. Navigate to the /opt Directory
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

> ### 6. Create a New User
>
> ```bash
> useradd sonar
> ```

> ### 7. Change Directory Ownership
>
> Change the ownership of the SonarQube directory to the 'sonar' user.
>
> ```bash
> chown sonar:sonar sonarqube-8.9.6.50800 -R
> ```

> ### 8. Modify Directory Permissions
>
> ```bash
> chmod 777 sonarqube-8.9.6.50800 -R
> ```

> ### 9. Switch to the 'sonar' User
>
> ```bash
> su – sonar
> ```

> ### 10. Navigate to /opt Directory Again
>
> ```bash
> cd /opt
> ```

> ### 11. Enter the SonarQube Directory
>
> ```bash
> cd sonarqube-8.9.6.50800
> ```

> ### 12. Navigate to the 'bin' Directory
>
> ```bash
> cd bin/
> ```

> ### 13. Navigate Further to the 'linux' Directory
>
> ```bash
> cd linux-x86-64/
> ```

> ### 14. Start SonarQube
>
> ```bash
> sh sonar.sh start
> ```

> ### 15. Check SonarQube Status
>
> ```bash
> sh sonar.sh status
> ```

> ### 16. Access SonarQube on a Web Browser
>
> Now, open a browser and navigate to `http:<public_ip>:9000`. 

> ### 17. Log In
>
> Use 'admin' as both the username and password.

> ### 18. Update Password
>
> After logging in, you will be prompted to create a new password. Ensure it's strong and securely stored.

> ### 19. Back to Jenkins
>
> Now, switch back to your Jenkins instance for further configurations.
> ### 20. Create a Jenkins Job
>
> Set up a new job named 'jenkins_Project'.

> ### 21. Go to EC2
>
> Switch to your EC2 instance for the next set of commands.

> ### 22. Install Git
>
> ```bash
> yum install git -y
> ```

> ### 23. Return to Jenkins
>
> Switch back to your Jenkins instance.

> ### 24. Access Global Tool Configuration
>
> Navigate to 'Manage Jenkins' -> 'Global Tool Configuration'.

> ### 25. Add Maven
>
> You'll be setting up Maven for your project.

> ### 26. Maven Setup - Name
>
> Set 'Name' as 'maven'.

> ### 27. Maven Setup - Version
>
> ```bash
> Set 'Version' as '3.8.6'.
> ```

> ### 28. Add Git Pipeline Code
>
> Below is the pipeline code for Git:
>
> ```groovy
> node{
>     stage("code"){
>         git "repo.git"
>     }
> }
> ```

> ### 29. Add Maven Pipeline Code
>
> Integrate Maven into the pipeline with the following code:
>
> ```groovy
> node{
>     stage("build"){
>         def mavenHome = tool name: "maven", type: "maven"
>         def mavenCMD = "${mavenHome}/bin/mvn"
>         sh "${mavenCMD} clean package"
>     }
> }
> ```

> ### 30. Integrate Sonar with Jenkins
>
> Perform a code quality test by integrating Sonar with Jenkins. 

> ### 31. Go to Sonar
>
> Switch to your SonarQube instance.

> ### 32. Access Account Security
>
> Navigate to 'My Account' -> 'Security'.

> ### 33. Generate Token
>
> Generate a new token by providing a name for it. Ensure you copy and save the generated token securely.

> ### 34. Return to Jenkins
>
> Switch back to Jenkins to configure the connection to SonarQube.

> ### 35. Navigate to Configuration in Jenkins
> 
> Go to 'Manage Jenkins' -> 'Configure System' -> 'SonarQube servers'.

> ### 36. Name the Server
>
> Set 'Name' as 'mysonar'.

> ### 37. Set Sonar Server URL
>
> Input your Sonar server URL in the 'Server URL' field.

> ### 38. Credentials Issue
>
> Initially, you won't be able to add credentials. Save the settings and then revisit the page.

> ### 39. Set Credential Kind
>
> Choose 'Secret Text' for the 'Kind'.

> ### 40. Input Secret Token
>
> In the 'Secret' field, paste the token you generated from SonarQube.

> ### 41. Add SonarQube Pipeline Code
>
> Here's the pipeline code to integrate SonarQube with Jenkins:
> 
> ```groovy
> node{
>     stage("test"){
>         withSonarQubeEnv('mysonar'){
>             def mavenHome = tool name: "maven", type: "maven"
>             def mavenCMD = "${mavenHome}/bin/mvn"
>             sh "${mavenCMD} sonar:sonar"
>         }
>     }
> }
> ```

> ### 42. Go to Sonar Again
>
> Return to your SonarQube instance.

> ### 43. Check Projects
>
> By this point, you should see a project listed in SonarQube where you can review the code quality.

> ### 44. Return to Jenkins
>
> Switch back to Jenkins for further configurations.

> ### 45. Setting up Nexus with Jenkins
>
> Integrating Nexus with Jenkins can be a bit challenging, so you'll be using 'Pipeline Syntax' for assistance.

> ### 46. Choose Nexus Artifact Uploader
>
> Select 'Nexus Artifact Uploader' from the 'Pipeline Syntax' options.

> ### 47. Set Nexus Version
>
> Set 'Version' as 'nexus3'.

> ### 48. Set Protocol
>
> Choose 'http' as the protocol.

> ### 49. Nexus Server URL
>
> Input your Nexus server URL (typically it'd be in the format `ip:8081`).

> ### 50. Set Up Nexus Credentials
>
> ```bash
> a. Set 'Kind' as 'Username with Password'.
> b. For 'Username', use 'admin'.
> c. Input your Nexus password in the 'Password' field.
> ```

> ### 51. Maven Details
>
> For 'GroupID', provide the group ID from your `pom.xml` file. Similarly, for 'Version', input the version from `pom.xml`.

> ### 52. Repository Creation Reminder
>
> You forgot to create a repository in Nexus. That's an essential step.

> ### 53. Go to Nexus
>
> Head over to your Nexus instance.

> ### 54. Access Settings in Nexus
>
> Click on 'Settings' and then navigate to 'Repositories'.

> ### 55. Create New Repository
>
> Click the 'Create repository' button.

> ### 56. Select Repository Type
>
> Choose 'maven2 (hosted)' for the repository type.

> ### 57. Name the Repository
>
> Provide a suitable name for your repository.

> ### 58. Deployment Policy Setting
>
> In the 'Hosted' section towards the bottom, choose 'Allow redeploy' under the 'Deployment policy'.

> ### 59. Return to Jenkins
>
> Switch back to your Jenkins dashboard.

> ### 60. Provide Repository Name in Jenkins
>
> Input the name of the repository you just created in Nexus.

> ### 61. Maven Details for Jenkins
>
> Enter the 'ArtifactID' from your `pom.xml` file. Similarly, provide the 'Type' from `pom.xml`.

> ### 62. Classifier Field in Jenkins
>
> You can leave the 'Classifier' field empty as it's not mandatory.

> ### 63. Provide Path in Jenkins
>
> For the 'Path', input `target/*.war`.

> ### 64. Generate Pipeline Script in Jenkins
>
> Click on the 'Generate Pipeline Script' button to get the required code snippet for Nexus.

> ### 65. Nexus Pipeline Code
>
> Add the provided Nexus pipeline code into your Jenkins pipeline:
> 
> ```groovy
> node{
>     stage("nexus"){
>         // Make sure to paste the generated code here...
>     }
> }
> ```

> ### 66. Verify Nexus Deployment
>
> After executing the build, ensure you can see a war file in Nexus.

> ### 67. Tomcat Deployment
>
> The final part of your pipeline is deploying to Tomcat.

> ### 68. Late Night Note
>
> Good night! Remember, it's 3 AM. Sleep is crucial; we can pick this up tomorrow.

> ### 69. Morning Greeting
>
> Good morning! Let's finish what we started.

> ### 70. Tomcat Deployment Using Pipeline Syntax
>
> For Tomcat, avoid writing the code directly. Instead, use Jenkins' 'Pipeline Syntax' and select 'SSH Agent'.

> ### 71. Copy .pem File for Production Environment
>
> Ensure you have the `.pem` file for your production environment handy.

> ### 72. SSH Credentials Setup in Jenkins
>
> Set up your SSH credentials in Jenkins:
> ```bash
> a. Choose 'SSH Username with private key' for the 'Kind'.
> b. Use 'ec2-user' as the 'Username'.
> c. Paste your `.pem` file content into the 'Private Key' field.
> ```

> ### 73. Generate Pipeline Syntax for SSH
>
> Click on 'Generate Pipeline Syntax' to get the required code snippet for SSH and Tomcat deployment.

> ### 74. SSH and Tomcat Deployment Pipeline Code
>
> Incorporate the provided SSH and Tomcat deployment code into your Jenkins pipeline:
> 
> ```groovy
> node{
>     stage("deploy"){
>         // Make sure to paste the generated SSH code here...
>         {
>             sh 'scp -o StrictHostKeyChecking=no /var/lib/Jenkins/workspace/job-name/target/war-file-name ec2-user@public_ip:/opt/apache-tomcat-9.0.74/webapps/'
>         }
>     }
> }
> ```

> ### 75. Explanation of SCP Command
>
> SCP stands for Secure Copy. The lengthy command provided simply copies the war file from Jenkins server to Tomcat. The provided path, `/var/lib/Jenkins/workspace/job-name/target/war-file-name`, is the source file path, while `ec2-user@public_ip:/opt/apache-tomcat-9.0.74/webapps/` is the destination path on the Tomcat server.

> ### 76. A Simpler Understanding
>
> You might be intimidated by the long command, but don't be. We're merely moving the `war` file from our Jenkins server to the Tomcat server. The source file path is `/var/lib/Jenkins/workspace/job-name/target/war-file-name`, and the destination is `ec2-user@public_ip:/opt/apache-tomcat-9.0.74/webapps/`.

> ### 77. Permission Denied Error
>
> You might encounter a 'Permission Denied' error, but don't fret.

> ### 78. Fixing the Permission
>
> Let's address this by going to the Tomcat server.

> ### 79. Navigate Directories in Tomcat
>
> Go back two directories using the command:
> ```bash
> cd ../..
> ```

> ### 80. Switch to the /opt Directory
>
> Use the following command:
> ```bash
> cd /opt/
> ```

> ### 81. Adjusting Permissions for Apache File
>
> It's essential to grant the 'ec2-user' the necessary permissions for the Apache file.

> ### 82. Change Ownership for Apache File
>
> Alter the ownership of the Apache file to 'ec2-user' with:
> ```bash
> chown ec2-user:ec2-user apache_file_name -R
> ```

> ### 83. Return to Jenkins
>
> Navigate back to your Jenkins dashboard.

> ### 84. Execute the Build
>
> Now, initiate the build process.

> ### 85. Celebrate Your Achievement
>
> "We won the war!" Revel in the success of your pipeline's successful execution.


