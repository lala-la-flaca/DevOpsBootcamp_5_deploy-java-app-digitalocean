# Cloud & IaaS Basics

## Description
This demo project is part of Module 5: Cloud & IaaS from Nana DevOps Bootcamp. It shows how to set up and configure a Linux server on DigitalOcean, deploy Nana's Java Gradle application, and implement security best practices.
While DigitalOcean is a paid service, first-time users receive free credits, which should be enough to complete this project.

<br />

## 🚀 Technologies Used

- <b>Digital Ocean: Cloud provider for hosting the application.</b>
- <b>Linux: Ubuntu for Server configuration and management.</b>
- <b>Java/Gradle: Nana's application and build tools.</b>


## 🎯 Features

- <b>Setup a droplet(VM) in Digital Ocean.</b>
- <b>Deploy and run a Java Gradle application on a DigitalOcean droplet.</b>
- <b>Implement security best practices.</b>
- <b>Create and configure a Linux user for secure access.</b>

## 🏗 Project Architecture
<img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/DigitalOcean_Java_App_Architecture.png"/>

## ⚙️ Project Configuration:
### Cloning Nana’s Java-Gradle Application Locally

To clone the Java-Gradle application from Nana DevOps Bootcamp, follow these steps:

1. Find the repository here: [Nana Bootcamp Repository](https://gitlab.com/twn-devops-bootcamp/latest/05-cloud/java-react-example)
2. Clone the repository:
   ```bash
   git clone https://gitlab.com/twn-devops-bootcamp/latest/05-cloud/java-react-example

### Creating a Droplet on Digital Ocean
1. Sign up for an account on [DigitalOcean](https://www.digitalocean.com).
2. Create a droplet:<br>
   a) Select **Create Droplet** from the Digital Ocean dashboard. <br>

      <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/create%20a%20droplet%201.png?raw=true"/>
    
   b) Select a region: Select the region closest to your location.<be>

      <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/Droplet%20region.png?raw=true"/>

   c) Select an image: Select the Ubuntu image.<br>

      <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/CreatingDropletChooseImage.png?raw=true"/>
     
     - Choose Size: <br>
       * Droplet type: Select Basic.<br>
       * CPU options: Select Regular SSD and the cheapest option.<br>

       <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/CreatingDropletCPU.png?raw=true"/>
   
   d) Select the SSH key  as the Authentication Method. <br>
    - Generate a New SSH Key (if required): If you do not have an existing SSH key, follow DigitalOceans's guide to create a new pair.
    - Use an existing SSH Key: if you already have a public SSK key pair, navigate to the .ssh folder in your local directory. Copy the public key and paste it into the appropriate field in DigitalOCean's interface.<br>

      <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/DropletSSH.png?raw=true"/>

   e) Select **Create Droplet**

### Configuring Firewall on Digital Ocean
Following security best practices, configure the firewall's inbound and outbound rules. In this case, you only allow inbound SSH access from your machine to the Droplet, restricting all other unnecessary connections.

1. Select the **Networking** option from the left panel, then choose **Firewall**.

   <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/SettingUpFirewall.png?raw=true"/>

2. Click on **Create Firewall**
  
3. Set the firewall rules for incoming traffic.<br>
   Allow SSH access from your machine by adding an inbound rule that allows traffic from the public IP address of your machine on port 22. Keep in mind that this IP changes when restarting your machine.

   <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/Firewall2.png?raw=true"/>
   
4. SSH into the droplet to verify that everything works as expected.

   <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/Access%20to%20Droplet.png?raw=true"/>

   
5. Update the package manager on the droplet.
   ```bash
       apt update
6. Install Java openjdk17 on the droplet, as this version is compatible with Nexus, which will be used in the following exercises.
   ```bash
       apt install openjdk-17-jre-headless
   ```
7. Navigate to the directory where the app is stored.
        
8. Build the Java application using Gradle from your machine.
    
   ```bash
       gradle build
   ```
9. Locate the .JAR file saved in the build directory under the libs folder.

     <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/BuildGradle%20and%20get%20jar%20file.png?raw=true"/>

    
10. Navigate to the location of the .jar file and copy the file to the droplet.
    
    ```bash
       scp <location .jar> <destination on droplet>
    ```
    <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/Transfering%20jar%20file%20to%20droplet.png?raw=true"/>
    
11. Navigate to the root directory on the droplet and confirm that the file has been successfully uploaded.
    
    <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/JarFile%20available%20on%20%20Droplet.png?raw=true"/>
    
12. Since Java is installed on the droplet (Step 6), execute the application.
    ```bash
       java -jar java-react-example.jar
    ```
    
    
13. Navigate to the **Networking** tab in the left menu, select Firewall, and click on the droplet's firewall.
    
    <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/SettingUpFirewall.png?raw=true"/>
    
14. Add a new rule that allows access on port 7071 from all IP addresses, as the app must be accessible to anyone.
    
    <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/Allowing%20access%20to%20port%207071.png?raw=true"/>
    
15. Open a browser and use your droplet's IP address:port
    
    <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/ApplicationRunningOnDropletPort.PNG?raw=true"/>


The application is running on DigitalOcean, but using the root account is not recommended. To follow best practices, create a Linux user with root privileges to start the application and assign only the  required permissions.

### Creating a Linux User on the Droplet.
1. Create a user on the droplet.
   ```bash
      adduser <new_user>
      adduser lala
    ```
2. Add the user to the sudo group
    ```bash
       sudo usermod -aG sudo lala
    ```
3. Create the .SSH directory for the new user.

   <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/CreatingSSHDirectoryNewUser.png?raw=true"/>
   
4. Add the authorized_keys file and copy the public key of your machine.

   <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/SSHpublicKey.png?raw=true"/>
   
5. Copy the file from the machine to the droplet  using the new user.

   <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/Copying%20the%20file%20to%20new%20user.png?raw=true"/>
   
6. Execute the application.

    <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/RunningAppfromNewUser.png?raw=true"/>

    
7. Access the app via: [Application Running on Digital Ocean](http://167.71.251.169:7071/)



    
 
     
  
























# Java-React Example

An example of how to use JS frontend to consume an endpoint written in Java.

## Frontend technologies

- [React](https://facebook.github.io/react/) - UI Library
- [Redux](http://redux.js.org/) - State container

## Additional information
 This project is a part of a [presentation](https://docs.google.com/presentation/d/1-yZhsM43cyWWDVn6EUtK_wc39FAv-19_jwsKXlTe2o8/edit?usp=sharing)

Related projects:

- [react-intro](https://github.com/mendlik/react-intro) - Introduction to react and redux.
- [java-webpack-example](https://github.com/mendlik/java-webpack-example) - Advanced example showing how to use a module bundler in  a Java project.

Tip: [How to enable LiveReload in IntelliJ](http://stackoverflow.com/a/35895848/2284884)

<hr/>
Original project can be found here: https://github.com/pmendelski/java-react-example 
