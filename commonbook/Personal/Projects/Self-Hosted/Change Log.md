**Changing Default Ports for Nextcloud Snap**

**Issue:** The Nextcloud Snap installation was using port 80, causing a conflict with other services.

**Solution:** Reconfigured the Snap-managed Nextcloud instance to use different ports for HTTP and HTTPS.

Steps Taken: 
1. Checked Current Ports: sudo snap get nextcloud ports 
2. Changed Ports: Updated the HTTP port to 8081: sudo snap set nextcloud ports.http=8081 Updated the HTTPS port to 8443: sudo snap set nextcloud ports.https=8443 
3. Restarted Nextcloud: sudo snap restart nextcloud 
4. Verified Changes: Checked that port 80 was now free: sudo lsof -i :80 Confirmed Nextcloud Snap was accessible on the new ports.

Outcome: Nextcloud is now running on custom ports (HTTP: 8081, HTTPS: 8443). Port 80 is available for other services, such as Nginx.