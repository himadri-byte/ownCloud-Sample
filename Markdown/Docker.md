# ownCloud Installation and Configuration with Docker 

## Introduction  

You can install ownCloud using Docker from the [official ownCloud Docker image](https://hub.docker.com/r/owncloud/server/tags/ "official ownCloud Docker image"). The official image works standalone for a quick evaluation, however, it is designed to be used in a docker-compose setup.  


## Docker Compose  

The configuration:

* Exposes ports 8080, allowing users for HTTP connections.

* Uses separate MariaDB and Redis containers.

* Mounts the data and MySQL data directories on the host for persistent storage.  

The following instructions are for local installation. For remote access, the value of OWNCLOUD_DOMAIN must be adapted.

1. Create a new project directory. Then copy and paste the sample `docker-compose.yml` from this page to the new directory.

2. Create a `.env` configuration file, that contains the required configuration settings. Only a few settings are required, these are:  

    * **`OWNCLOUD_VERSION`**: Provide ownCloud Version. Example: `latest`  

    * **`OWNCLOUD_DOMAIN`**: Provide the ownCloud domain. Example: `localhost:8080`  

    * **`ADMIN_USERNAME`**: Provide the admin username. Example: `admin`  

    * **`ADMIN_PASSWORD`**: Provide the admin user’s password. Example: `admin`  

    * **`HTTP_PORT`**: Provide the HTTP port to bind. Example: `8080`  

    **NOTE**  

    ADMIN_USERNAME and ADMIN_PASSWORD will not change between deploys even if you change the values in the .env 
    file. To change them, you’ll need to do docker volume prune, which will delete all your data.  

After configuring, you can start the container, using your preferred Docker command-line tool. The example below shows how to use Docker Compose.  

    # Create a new project directory
    sudo mkdir owncloud-docker-server

    cd owncloud-docker-server

    # Copy docker-compose.yml from the GitHub repository
    wget https://raw.githubusercontent.com/owncloud/docs/master/modules/admin_manual/examples/installation/docker/docker-compose.yml

    # Create the environment configuration file
    cat << EOF > .env
    OWNCLOUD_VERSION=10.6
    OWNCLOUD_DOMAIN=localhost:8080
    ADMIN_USERNAME=admin
    ADMIN_PASSWORD=admin
    HTTP_PORT=8080
    EOF

    # Build and start the container
    sudo docker-compose up -d  

When the process completes, check that all the containers have successfully started, by running `sudo docker-compose ps`.

In the results, you can see that the database, ownCloud, and Redis containers are running, and that ownCloud is accessible via port 8080 on the host machine.  

## Log In  

1. To log in to the ownCloud UI, open `http://localhost:8080` in your browser. The ownCloud login screen will appear. ![Login Image](https://doc.owncloud.com/server/10.6/admin_manual/_images/docker/owncloud-ui-login.png "Login Image")  

2. Enter the user name and passwords in the provided fields. These should be the same user name and passwords that you used in the `.env` earlier.  

## Other Configuration Options  

Other configurations for ownCloud installation using Docker are available in the [detailed installation guide](https://doc.owncloud.com/server/10.6/admin_manual/installation/docker/ "detailed installation guide"). 
