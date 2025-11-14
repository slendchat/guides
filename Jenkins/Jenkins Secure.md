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
7.  Configure FireWall