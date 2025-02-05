
**1. Plan and Prepare**

**Host Machine Resources**
- 

	• Ensure your Hyper-V host has sufficient CPU, RAM, and storage.

• **Network Design**

• Create or confirm an **External Virtual Switch** in Hyper-V.

• Decide on static vs. DHCP IP addressing and hostnames.

• **Services Outline**

• Which VMs will host which services? (Reverse proxy, Keycloak, XWiki, Nextcloud, Chat, Database, etc.)

• **Obtain OS ISO**

• Typically Ubuntu 22.04 LTS (server edition) or Debian 12.

  

**2. Create a Base Ubuntu VM (Template)**

1. **New VM in Hyper-V**

• Name: Ubuntu-Template

• Generation 2 if supported

• Assign CPU, RAM (≥2GB)

• Attach Ubuntu Server ISO

2. **Install Ubuntu Server**

• Create an admin user

• sudo apt update && sudo apt upgrade -y

3. **Enable SSH**

• sudo apt install -y openssh-server

• sudo systemctl enable ssh && sudo systemctl start ssh

4. **Export or Create Checkpoint**

• This becomes your “golden image” or template.


**3. Create the Individual VMs**


Using the Ubuntu-Template (clone or export/import):

1. **VM #1: Reverse Proxy + Keycloak**

• Hostname: proxy-keycloak

• Static IP recommended

2. **VM #2: Database Server**

• Hostname: db-server

• Install PostgreSQL or MariaDB

3. **VM #3: XWiki**

• Hostname: xwiki

• Install XWiki (Docker or WAR/Tomcat)

• Connect to DB on VM #2

4. **VM #4: Nextcloud** (optional)

• Hostname: nextcloud

• Install Nextcloud

• Connect to DB on VM #2

• Integrate NAS (as external storage or data directory)

5. **VM #5: Chat** (optional)

• Hostname: chat

• Install Mattermost or Rocket.Chat (Docker or native)

• Connect to DB on VM #2

  

**4. Configure Reverse Proxy & DNS**

• **Nginx (or Traefik) on VM #1**

• Reverse proxy for SSL termination / routing

• id.example.local → Keycloak

• wiki.example.local → XWiki

• cloud.example.local → Nextcloud

• chat.example.local → Chat

• **DNS or /etc/hosts**

• If local DNS is available, create A records

• Otherwise, use /etc/hosts on client machines or each VM

• **SSL Certificates**

• Use Let’s Encrypt (if publicly accessible) or self-signed / internal CA

  

**5. Install & Configure Keycloak for SSO**

1. **Deploy Keycloak** on VM #1

• Native or Docker container

2. **Reverse Proxy**

• id.example.local → Local Keycloak instance on port 8080

3. **Create Realms & Clients**

• Add a realm (e.g., mycompany)

• Create clients for XWiki, Nextcloud, Chat, etc.

  

**6. Set Up XWiki (VM #3)**

1. **Install XWiki**

• Docker or Tomcat + WAR

• Connect to DB on VM #2

2. **Configure Reverse Proxy**

• wiki.example.local → XWiki VM port (e.g., 8080)

3. **SSO Integration** (optional)

• Use [OpenID Connect Authenticator Extension](https://extensions.xwiki.org/xwiki/bin/view/Extension/OpenID%20Connect/)

  

**7. Set Up Nextcloud (VM #4)**

1. **Install Nextcloud**

• Docker or LAMP stack

• Connect to DB on VM #2

2. **Reverse Proxy**

• cloud.example.local → Nextcloud VM

3. **NAS Integration** (optional)

• External Storage or store Nextcloud data on the NAS

4. **Keycloak SSO** (optional)

• Use Nextcloud’s OIDC or SAML plugin

  

**8. Set Up Chat (VM #5) [Optional]**

1. **Install Mattermost / Rocket.Chat / Matrix**

• Docker or native

2. **Reverse Proxy**

• chat.example.local → Chat VM

3. **SSO**

• OIDC or SAML client in Keycloak

  

**9. Test SSO and Workflows**

1. **Keycloak**

• Create test users

• Check login flows for XWiki, Nextcloud, Chat

2. **Connectivity**

• Verify each service at http://<subdomain>.example.local

3. **Permissions**

• Map Keycloak roles to each application if needed

  

**10. Backups & Maintenance**

1. **Database Backups**

• Schedule dumps (pg_dump, mysqldump) on VM #2

2. **VM Snapshots**

• Hyper-V checkpoints (for PoC)

3. **App Updates**

• Docker: docker pull ...

• Native: apt upgrade, WAR updates, etc.

4. **Monitoring** (optional)

• Consider Prometheus + Grafana or another monitoring solution

  

**11. Documentation & Implementation**

• **Create Guides** for each service and step.

• **Document** IP addresses, hostnames, firewall rules, credentials.

• **Implement** carefully, verifying each component in turn.

  

**End of Notes**

  

Use this outline as your “master plan” in Obsidian, and then create individual notes or sub-pages branching off each major heading (e.g., one note for “Install Keycloak,” another for “Configure XWiki,” etc.). This ensures everything is well-documented and easy to reference.