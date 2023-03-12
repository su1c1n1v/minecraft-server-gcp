
<div align="center">
  <h1>Minecraft Server GCP</h1>

  ![Alt Text](https://media.giphy.com/media/2PWBLDJ2KtB1X6o9vY/giphy.gif)
  
  <a href="#about">About</a> •
  <a href="#getting-started">Getting Started</a> •
  <a href="#built-with">Built With</a> •
  <a href="#author">Author</a> •
</div>

## About

In this project we are going to implement a Minecraft server in the cloud using VM instance and Minecraft docker image.

## Getting Started

### Create project in the GCP

First it is required to [create a project](https://cloud.google.com/resource-manager/docs/creating-managing-projects) in the GCP.

Go to the Compute Engine in the menu and click in VM instances, after that create a instance with your region and select a name for your VM, in the Machine configurantion select Series E2 and Machine type e2-medium (it is enought to run the server).

![image](https://user-images.githubusercontent.com/46250524/224546924-e183aaba-9819-4818-b6b9-7e2492423c3d.png)
---

In the "Container" click to DEPLOY CONTAINER
- Field "Container image" write "registry.hub.docker.com/itzg/minecraft-server";
- Check the "Allocate a buffer for STDIN" and "Allocate a pseudo-TTY";
- In the "Environment variables" the only mandatory variable is the "EULA", you can search in the documentation of the [image](https://github.com/itzg/docker-minecraft-server) if you want to customize.

![image](https://user-images.githubusercontent.com/46250524/224548206-fdb0ad15-8432-4dfb-952f-ab3f323ad805.png)

--- 

- Create a Volume mount to save the information of the server

![image](https://user-images.githubusercontent.com/46250524/224547854-acc267b2-e7e4-42b9-9b06-7314cece4240.png)

---

In the "Advanced options" select the sub-area "Networking" and create a Network tags, It will be used in the future to create a firewall to access the server. 

![image](https://user-images.githubusercontent.com/46250524/224547170-98c53037-2a45-427b-b89e-be6e49d19f1b.png)

--- 

After configure the VM and create the VM, go to the VM instances and click in the "Set up firewall rules" and click in "CREATE FIREWALL RULE"
In the Create a firewall rule
- Write the name of the rule
- Set the priority for 1000
![image](https://user-images.githubusercontent.com/46250524/224549142-92429f6a-8566-41dd-9a53-b1ef842e4359.png)

- In the field "Target tags" write the name of the tag that you wrote in the Network tags in the creation of the VM
![image](https://user-images.githubusercontent.com/46250524/224549198-4b27adf4-0e8c-4610-aa09-3a74d66ed9a8.png)

- In Direction of traffic select "Ingress"
![image](https://user-images.githubusercontent.com/46250524/224549164-e637394b-22ea-4d90-9faf-3c316fcfd5fe.png)

- In Protocols and ports, select Specified protocols and ports, select TCP and write the port 25565
![image](https://user-images.githubusercontent.com/46250524/224549185-2d684ff5-d8e1-4c50-a8ea-779c617bc9f7.png)

---

After create the Rule go to VM instances and copy the External IP and write in your Minecraft, in the end of the External API, add the port (25565).


## Built with

- [Google Cloud Platform](https://cloud.google.com/)
- [Docker](https://www.docker.com/)
- [Minecraft image](https://github.com/itzg/docker-minecraft-server)

## Author

- **Vinícius Costa** - [su1c1n1v](https://github.com/su1c1n1v)
