# Docker Dock
This like docker documentation but to get started

## To Install docker
`curl -sSL https://get.docker.com | sh`<br>
Executes code from [this website]("https://get.docker.com")<br>
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
[GitHub](https://github.com/ConSol/docker-headless-vnc-container/) [Docker hub](https://hub.docker.com/r/aicampbell/vnc-ubuntu18-xfce)
```sh
sudo docker run -d -p 5901:5901 -p 6901:6901 --user 0 --hostname debian-desktop consol/debian-xfce-vnc
```

Based on these tutorials:
* [How to install Docker (and Portainer) on a RaspberryPi and run millions of apps on your RaspberryPi!](https://youtu.be/O7G3oatg5DA)
* [How to Update Portainer Fast, Simple, and Easy Guide](https://youtu.be/M365jgJ0O2E)
