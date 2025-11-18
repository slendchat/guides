# Securing Jenkins server

### Core and Outdated Plugin Updates
1. Regularly **update Jenkins Core** to the **latest version**.
2. Update **Plugins** to the **latest versions** possible.
3. Install **only required** plugins.

### Operating system Hardening
1. Open only HTTP ports and Jenkins Agent port(JNLP)
2. Jenkins runs under jenkins user
3. Harden permission to JENKINS_HOME
4. No sudo for jenkins user
5. Use HTTPS for webui
6. Block server from public access
7.  Configure Firewall
The rule - secure the server as much as the servers where artifacts are deployed.

### Authentication
Do not use builtin methods for authorization, instead use third party provider like **LDAP**.

### Authorization 
Do not use builtin methods again.
Use plugins:
1. Matrix Authorization Strategy
2. Role-based Authorization Strategy
Define the privileges of anon, authenticated or specific user.
Additionally you can define privileges per project.
Check this tutorial: https://www.youtube.com/watch?v=iPBNEWUocjs

### Security (Mis)configurations
No code execution on **controller node**.
Use proper network segmentation.
Limit the permissions to needed scope.

### Hardening inbound connections
Use JNLP agents with fixed open port 50000.
Agent initiate connection to the Controller, the JNLP port should be configured to accept connections on port 50000.
Make agents use TLS encryption
Disable SSHD
Markup Formatter - safe html
Run code under the container if possible.
### Limit the Agent permissions
Agents should run the code with configured which user, hence what permissions, will run the build.

### Secure Credentials
Use `Folder plugin` to define credentials under specific folders.
Only pipelines under the specified folder can access its credentials.
To limit users access to those credentials use `Role-based Authorization Plugin`

### Audit logs
Use plugin `Audit Trail` allow writing or sending logs to remote server.

## Source
https://cycode.com/blog/jenkins-security-best-practices/
