# Linux Dock
Small linux knowledge base
**WARNING:** most of the instructions provided here are for arm processors only

## To Install docker
`curl -sSL https://get.docker.com | sh`<br>
Executes code from [this website](https://get.docker.com)<br>
Run the command `docker` to make sure it was installed correctly, if it was it should list the command's documentation<br>
To allow a user to access docker: `sudo usermod -aG docker <username>`<br>

## To Install Portainer
`sudo docker pull portainer/portainer-ce:linux-arm`<br>

**To run portainer**<br>
`sudo docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:linux-arm`<br>
If you want to use another port change the 9000s to the port you want to use<br>

**To access portainer**
In your browser go to `http://raspberrypi.local:9000` (if you used another port replace 9000 with that)
If that doesnt work simply go to your raspberry pi's ip with the port

Das it the ui is cool :)

## To update portainer
Stop portainer
```sh
docker stop portainer
```
Remove the container
```sh
docker rm portainer
```
Remove the outdated image
```sh
docker rmi <image-id>
```

Install the new version with the `latest` tag
```sh
 docker run -d -p 8000:8000 -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```
If theres a not found error look at [this](https://github.com/portainer/portainer/issues/4143)

## To install Debian desktop on docker
_Unable to launch minecraft_
**OUTDATED, use below instead**
[GitHub](https://github.com/ConSol/docker-headless-vnc-container/) [Docker hub](https://hub.docker.com/r/aicampbell/vnc-ubuntu18-xfce)
```sh
sudo docker run -d -p 5901:5901 -p 6901:6901 --user 0 --hostname debian-desktop consol/debian-xfce-vnc
```
## To run ubuntu with LXQT desktop
_Could run minecraft, LWJGL doesnt load properly_
```sh
sudo docker run --detach -e USER=root -e RESOLUTION=1280x720 -p 5900:5900 carlonluca/vnc-desktop:jammy-lxqt
```
Then connect to port 5900 via VNC
You can also change the resolution (duh)

_Original [github](https://github.com/carlonluca/docker-vnc-desktop) [docker image](https://hub.docker.com/r/carlonluca/vnc-desktop)_

## To run xfce4 thru vnc in ubuntu server
_Unable to launch minecraft_
### Setup
Install required packages
```sh
sudo apt install xfce4 xfce4-goodies xfonts-75dpi xfonts-100dpi
```
Generate config files
```sh
vncserver
vncserver -kill :1 # :1 is the monitor index thing
```
Change startup config file
```sh
# Backup the original
mv ~/.vnc/xstartup ~/.vnc/xstartup.bak

# Create and edit the new one
nano ~/.vnc/xstartup
```
In the new `xstartup` file write 
```
#!/bin/bash
xrdb $HOME/.Xresources
startxfce4 &
```
Set the correct permissions for the new file
```sh
chmod +x ~/.vnc/xstartup
```
Create the Xresources file (*might not be necessary*)
```sh
sudo touch /root/.Xresources
```

**To start it**
```
vncserver
```
**To stop it**
```
vncserver -kill :1
```
**To connect to it**
use a vnc client and connect to the 5901 port with the specified password
**To read display 1's log**
```
cat /home/beveledcube/.vnc/ubuntu:1.log
```

[Original Digital Ocean tutorial](https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-vnc-on-ubuntu-22-04) ( Secure connection part was skipped )

Based on these tutorials:
* [How to install Docker (and Portainer) on a RaspberryPi and run millions of apps on your RaspberryPi!](https://youtu.be/O7G3oatg5DA)
* [How to Update Portainer Fast, Simple, and Easy Guide](https://youtu.be/M365jgJ0O2E)
