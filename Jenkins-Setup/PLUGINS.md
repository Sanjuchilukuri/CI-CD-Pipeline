# Jenkins Plugins Guide

This guide provides an overview of the crucial plugins we've integrated into our Jenkins setup, their purposes, and general setup steps.

## 1. SonarQube Scanner

### Purpose:
SonarQube Scanner is used for scanning source code and identifying code quality issues. It integrates with SonarQube to push scan results for further analysis.

### Installation:
1. Navigate to 'Manage Jenkins' > 'Manage Plugins' > 'Available'.
2. Search for "SonarQube Scanner".
3. Install without restart.

### Configuration:
- In Jenkins, go to 'Manage Jenkins' > 'Configure System'.
- Under 'SonarQube servers', add your SonarQube instance details.
- Save configurations.

## 2. Nexus Artifact Uploader

### Purpose:
This plugin allows Jenkins jobs to deploy artifacts to Nexus Repository Manager 3.x, making artifact storage and management more straightforward.

### Installation:
1. Navigate to 'Manage Jenkins' > 'Manage Plugins' > 'Available'.
2. Search for "Nexus Artifact Uploader".
3. Install without restart.

### Configuration:
- Define a new Nexus repository target in your Jenkins job configurations.
- Provide necessary credentials and repository details.

## 3. SSH Agent

### Purpose:
The SSH Agent plugin allows for the usage of SSH agent forwarding with Jenkins' `ssh` command, facilitating secured communication and file transfer between servers.

### Installation:
1. Navigate to 'Manage Jenkins' > 'Manage Plugins' > 'Available'.
2. Search for "SSH Agent".
3. Install without restart.

### Configuration:
- In your pipeline or job configuration, use `sshagent(credentials: ['my-credentials-id'])` to wrap commands requiring SSH authentication.

## Tips:
- Always keep your plugins updated to the latest versions to benefit from new features, improvements, and security patches.
- Backup your Jenkins configuration before making significant changes or updates.
- Ensure that any new plugins you add are compatible with your Jenkins version and other plugins to avoid conflicts.

---

Adjust the content above based on your specific configurations and preferences. Remember, clarity is crucial for documentation. Readers should quickly understand the purpose of each plugin, why it's essential, and any high-level steps or best practices associated with its use.
