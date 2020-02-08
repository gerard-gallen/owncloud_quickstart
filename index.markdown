---
layout: default
author: Gerard Gallen
Date: 2020-02-08
---
## Installation  and Configuration

 1. Download [Docker](https://docs.docker.com/docker-for-windows/install/) and a Docker command-line tool for your system.
  >Note: The examples in this guide use  [Docker Compose](https://docs.docker.com/compose/).  The Docker Desktop installation comes with it already installed.
 2. Download the [the official ownCloud Docker image](https://hub.docker.com/r/owncloud/server/).
 3. Create a new project directory and download [ownCloud’s docker-compose.yml file](https://raw.githubusercontent.com/owncloud/docs/master/modules/admin_manual/examples/installation/docker/docker-compose.yml) into the directory.
 4. Create a `.env` configuration file.
>**Note:** The following settings are required.
>
|  Setting |  Option  |  Example |
|:---------|:----------|:----------|
|`OWNCLOUD_VERSION`| The OwnCloud version | latest|
|`OWNCLOUD_DOMAIN`| The ownCloud domain|`localhost`|
|`ADMIN_USERNAME`| The admin username|`admin`|
|`ADMIN_PASSWORD`| The admin password |`admin` |
|`HTTP_PORT`| The HTTP port to bind to |`8080`|
 5. Build and start the container in your Docker command-line tool.
      ```
    # Create a new project directory
    mkdir owncloud-docker-server

    cd owncloud-docker-server

    # Copy docker-compose.yml from the GitHub repository
    wget https://raw.githubusercontent.com/owncloud/docs/master/modules/admin_manual/examples/installation/docker/docker-compose.yml

    # Create the environment configuration file
    cat << EOF > .env
    OWNCLOUD_VERSION=10.4
    OWNCLOUD_DOMAIN=localhost
    ADMIN_USERNAME=admin
    ADMIN_PASSWORD=admin
    HTTP_PORT=8080
    EOF

    # Build and start the container
    docker-compose up -d
```
 6. Run `docker-compose ps` to verify that all the containers have successfully started.
 >**Note:** Your output should be similar to the below example.
    ```
Name                Command                       State             Ports
__________________________________________________________________________________________
server_db_1         /usr/bin/entrypoint/bin/s …   Up                3306/tcp
server_owncloud_1   /usr/local/bin/entrypoint …   Up                0.0.0.0:8080->8080/tcp
server_redis_1      /bin/s6-svscan /etc/s6        Up                6379/tcp
```
> **Note:**  Docker exposes ports 8080, allowing for HTTP connections, and mounts the data and MySQL data directories on the host for persistent storage.

That's it. Your installation is now complete.  Wait a few minutes for ownCloud to be fully accessible through the web UI.  

## Logging In to OwnCloud
![The ownCloud UI via Docker](https://doc.owncloud.com/server/10.4/admin_manual/_images/docker/owncloud-ui-login.png)
 1. Open a web browser and go to `http://localhost/8080`
 2. Enter the username and password you stored in `.env` file earlier.

 You are now up and running and can begin to use ownCloud.

## Add a User Account

 1. Log in as **admin** to your ownCloud account.
 2. Select **users** in the top menu.
 3. Enter the new user’s **Login Name** and  **E-Mail**.
 4. Assign **Group** membership (optional).
 5. Click the **Create** button.
 ![image](https://doc.owncloud.com/server/10.3/admin_manual/_images/configuration/user/users-page-new-user.png)

  > **Note:** Login names may contain letters (a-z, A-Z), numbers (0-9), dashes (-), underscores (\_), periods (.) and at signs (@).  Click the gear icon on the lower left sidebar to view the available settings for each user.

   ![image](https://doc.owncloud.com/server/10.3/admin_manual/_images/configuration/user/users-page-gear.png)

## Using the Desktop Client

1.  Go to the  [ownCloud download page](https://owncloud.com/download/#desktop-clients) and download the  desktop client for your system.
2.  Run the program.
3.  Enter the server address configured (http://localhost/8080) and click **Next**.  
    ![ownCloud client configuration](https://docs.bitnami.com/images/img/apps/owncloud/configure-client-1.png)
4.  Enter a valid username and the given password.
5.  Specify whether to **Sync everything from server** or **Choose what to sync**.
6. Enter a location for your local files to be stored and choose whether to **Keep local data** or **Start a clean sync**.
![ownCloud client configuration](https://docs.bitnami.com/images/img/apps/owncloud/configure-client-3.png)
7.  Click **Connect** and then **Finish** to save the settings.

## Using the Mobile Client

1.  Go to your **Personal** page in the ownCloud Web interface to find links for the Android and iOS mobile clients.
>**Note:** You can also visit the  [ownCloud download page](https://owncloud.org/download/).
2.  Complete the wizard to set the optional security features, GIF Support, and to upload a picture.
>**Note:** On first use the mobile app shows a configuration screen.
3.  Enter your server URL (`http://localhost/8080`), login name, and password.![ownCloud Android App: Add a new account](https://doc.owncloud.com/android/_images/android-2.png)
4. Click **Connect**.
>**Note:** For better security, your ownCloud server should be SSL-enabled to connect through HTTPS.  If your server has a self-signed certificate click the  **YES**  button to accept the certificate and complete your account setup. The app opens on the **All Files**  screen.
5.  Click the main menu in the top left to manage the core features of the app or choose to add content.  
    ![ownCloud Android App: All files overview](https://doc.owncloud.com/android/_images/android-all-files-overview.png)
