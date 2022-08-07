# Welcome to the Anythink Market repo

To start the app use Docker. It will start both frontend and backend, including all the relevant dependencies, and the db.

Please find more info about each part in the relevant Readme file ([frontend](frontend/readme.md) and [backend](backend/README.md)).

## Development

When implementing a new feature or fixing a bug, please create a new pull request against `main` from a feature/bug branch and add `@vanessa-cooper` as reviewer.

## First setup
**[TODO 07/08/2022 @vanessa-cooper]:** To setup the environment we need to clone the repository and install docker on your local machine.
To install docker on the Ubuntu steps are mentioned below. If you have any other platform please refer docker documentation https://docs.docker.com/engine/install/   as per your system (like: Mac, Windows , Linux ).
### Clone repository

    $ git clone https://github.com/ObelusFamily/Anythink-Market-1zk8t.git

### Setup docker on Ubuntu

 1. **Uninstall old versions if any**
    - ```$ sudo apt-get remove docker docker-engine docker.io containerd runc```
 4. **Setup the repository**
	- Update the `apt` package index and install packages to allow `apt` to use a repository over HTTPS:
      - ```$ sudo apt-get update```
      - ```$ sudo apt-get install ca-certificates curl gnupg lsb-release```
     - Add Docker’s official GPG key:
        - ```$ sudo mkdir -p /etc/apt/keyrings```
        - ```curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg```
     - Use the following command to set up the repository:
```
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
 3. **Install Docker Engine**
      - ```$ sudo apt-get update```
      - ```$ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin```
 ### Post-installation steps for Linux
 1. **Manage Docker as a non-root user:**
    - Create the `docker` group.
      - ```$ sudo groupadd docker```
    - Add your user to the `docker` group.
      - ```$ sudo usermod -aG docker $USER```
    - Activate the changes to groups:
      - ```$ newgrp docker ```
    - Verify that you can run `docker` commands without `sudo`.
      - ```$ docker run hello-world```

 2. **Configure Docker to start on boot**
	- To enable
      - ```$ sudo systemctl enable docker.service```
      - ```$ sudo systemctl enable containerd.service```
	- To disable
      - ```$ sudo systemctl disable docker.service```
      - ```$ sudo systemctl disable containerd.service```
 3. **Configure Log Rotation (JSON File logging driver)**
	- `sudo nano /etc/docker/daemon.json`
	- Write below json object to file and save
```
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3" 
  }
}
```
   - Restart Docker for the changes to take effect for newly created containers. Existing containers do not use the new logging configuration.
      - ```docker run --log-driver json-file --log-opt max-size=10m alpine echo hello world```

You can verify docker is ready by running the following commands in your terminal: `docker -v` and `docker-compose -v`.

Then, **run `docker-compose up` from the project root directory** to load Anythink's backend and frontend.
