# Docker Compose Deployment Documentation

**Application:** Uptime Kuma
**Project:** Docker Compose – Project 2

## Overview

This documentation explains how to deploy **Uptime Kuma**, a self-hosted monitoring tool, using **Docker Compose**. The steps cover setting up the project directory, defining environment variables, creating the Docker Compose configuration, starting the service, and verifying that it is running correctly.

---

## Step 1: Prepare the Project Folder

1. Ensure Docker and Docker Compose are installed on your system.
2. Open a terminal window.
3. Create a new directory for the deployment:

   ```
   mkdir kuma-monitoring-project
   ```
4. Move into the newly created directory:

   
   cd kuma-monitoring-project
   


## Step 2: Configure Environment Variables

To make the configuration easier to manage, an environment file is used.

1. Create the `.env` file using a text editor:

   
   nano .env
   
2. Add the following line to specify the external port:

   
   KUMA_PORT=3002
   
3. Save the file and exit the editor.

This approach allows the port number to be changed later without editing the Docker Compose file directly.



## Step 3: Create the Docker Compose Configuration

1. Create the `docker-compose.yml` file:

   ```
   nano docker-compose.yml
   ```
2. Insert the configuration below:

   ```yaml
   version: "3.9"

   services:
     uptime-kuma:
       image: louislam/uptime-kuma:latest
       container_name: uptime-kuma-service
       ports:
         - "${KUMA_PORT}:3001"
       volumes:
         - kuma-data:/app/data
       restart: unless-stopped

   volumes:
     kuma-data:
   ```
3. Save the file and exit.

This configuration:

* Pulls the official Uptime Kuma image
* Maps a custom host port to the container
* Uses a named volume to store persistent data
* Automatically restarts the container if it stops



## Step 4: Start the Application

Deploy the service in detached mode by running:


docker compose up -d


Docker will download the required image (if not already present) and start the container in the background.



## Step 5: Verify the Deployment

After deployment, confirm that everything is working as expected.

1. **Check container logs:**

   ```
   docker compose logs
   ```

   This helps verify that the application started without errors.

2. **Confirm container status:**

   ```
   docker compose ps
   ```

   The service should appear as running with the correct port mapping.

3. **Verify the volume was created:**

   ```
   docker volume ls | grep kuma-data
   ```

   This confirms persistent storage is set up correctly.



## Step 6: Access the Web Interface

Open a web browser and navigate to:


http://localhost:3002


You should see the Uptime Kuma dashboard, where monitors can be created and managed.



## Conclusion

This deployment demonstrates how Docker Compose can be used to quickly and reliably run a monitoring service. By separating configuration into environment variables and using persistent volumes, the setup is flexible, maintainable, and suitable for long-term use.

* Rewrite it to sound **more advanced / professional**
* Format it for **GitHub Pages (Markdown)** or **Word (.docx)**
