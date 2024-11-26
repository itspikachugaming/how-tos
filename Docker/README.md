# Docker
Docker is a really powerful software that you can use to run many [different softwares](https://hub.docker.com/). Docker containers are like Virtual Machines (vm) since you can just stop the container and remove it whenever you like without any messy remains of the software but they use less resources so its perfect for less powerful computers like the raspberry pi. 

## Installing Docker
### Step 1 - update our system (as always :) )
Firstly, with any installation, update and upgrade all of our packages:

```
sudo apt update && sudo apt upgrade
```
### Step 2 - running the docker installation script
Time to install docker! To do this, run this script from docker to download and install it to your machine:

> [!NOTE]
> With anything on the internet, ALWAYS look at the script before downloading!

```curl -sSL https://get.docker.com | sh```

### Step 3 - Adding permissions to pi
When the install is complete, you will this:
```
================================================================================

To run Docker as a non-privileged user, consider setting up the
Docker daemon in rootless mode for your user:

    dockerd-rootless-setuptool.sh install

Visit https://docs.docker.com/go/rootless/ to learn about rootless mode.


To run the Docker daemon as a fully privileged service, but granting non-root
users access, refer to https://docs.docker.com/go/daemon-access/

WARNING: Access to the remote API on a privileged Docker daemon is equivalent
         to root access on the host. Refer to the 'Docker daemon attack surface'
         documentation for details: https://docs.docker.com/go/attack-surface/

================================================================================
```
Running that gives me this error:

```
pi@raspberrypi:~ $ dockerd-rootless-setuptool.sh install
[ERROR] Missing system requirements. Run the following commands to
[ERROR] install the requirements and run this tool again.

########## BEGIN ##########
sudo sh -eux <<EOF
# Install newuidmap & newgidmap binaries
apt-get install -y uidmap
EOF
########## END ##########
```
Now, I cant be bothered to figure that out so I have found a another way to get the user permissions:

```
sudo setfacl -m user:pi:rw /var/run/docker.sock
```
> Replace `pi` with the user of your linux user (found before the "@" in terminal line or typing in `whoami` in terminal)

## Installing Portainer - "But I dont like the terminal" (optional)
Firstly, the terminal is the best place to be but I know some of you would like to see things visually so we are going to install a GUI that you can access in a web browser

### Step 1 - downloading portainer
Wow this is exciting, this will be our first Docker container! We will firstly download the conainer image:
```
docker pull portainer/portainer-ce:linux-arm
```
> Learn:
> 
> `docker`: this tells the computer to use the docker software
> 
> `pull`: this tells the docker software to download a image from the internet
> 
> `-ce`: this tells the docker that we want to download the community edition of portainer
> 
> We are adding `:linux-arm` because we are on a linux machine running on the arm architecture (raspberry pi)

### Step 2 - installing portainer

```
docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:linux-arm
```



[YouTube](https://youtu.be/O7G3oatg5DA)
