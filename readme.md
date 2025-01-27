# Cloud & IaaS Basics

## Description
This demo project is part of Module 5: Cloud & IaaS from Nana DevOps Bootcamp. It shows how to set up and configure a Linux server on DigitalOcean, deploy Nana's Java Gradle application, and implement security best practices.
While DigitalOcean is a paid service, first-time users receive free credits, which should be enough to complete this project.

<br />

## Technologies Used

- <b>Digital Ocean: Cloud provider for hosting the application.</b>
- <b>Linux: Ubuntu for Server configuration and management.</b>
- <b>Java/Gradle: Nana's application development and build tools.</b>


## Features

- <b>Setup a droplet(VM) in Digital Ocean.</b>
- <b>Deploy and run a Java Gradle application on a DigitalOcean droplet.</b>
- <b>Implement security best practices.</b>
- <b>Create and configure a Linux user for secure access.</b>

## Project Architecture
<img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/DigitalOcean_Java_App_Architecture.png"/>

## Project Configuration:
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
   b) Select a region: Select the region closest to your location.<br>
   c) Select an image: Select the Ubuntu image.<br>
     - Choose Size: <br>
       * Droplet type: Select Basic.<br>
       * CPU options: Select Regular SSD and the cheapest option.<br>
       
   d) Select the SSH key  as the Authentication Method. <br>
    - Generate a New SSH Key (if required): If you do not have an existing SSH key, follow DigitalOceans's guide to create a new pair.
    - Use an existing SSH Key: if you already have a public SSK key pair, navigate to the .ssh folder in your local directory. Copy the public key and paste it into the appropiate field in DigitalOCean's interface.<br>

   e) Select **Create Droplet**

### Configuring Firewall on Digital Ocean
Following security best practices, configure the firewall's inbound and outbound rules. In this case, you only allow inbound SSH access from your machine to the Droplet, restricting all other unnecessary connections.
1. Select the **Networking** option from the left panel, then choose **Firewall**.
2. Click on **Create Firewall**
3. Set the firewall rules for incoming traffic.<br>
   Allow SSH access from your machine by adding an inbound rule that allows traffic from the public ip address of your machine on port 22.
4. SSH into the droplet to verify that everything is working as expected.
5. Update the package manager on the droplet.
   ```bash
       apt update
7. Install Java openjdk8 on the droplet, as this version is compatible with Nexus, which will be used in the following exercises.
   ```bash
       apt install openjdk-8-jre-headless
   ```
8. Navigate to the directory where the app is stored.
9. Build the Java application using Gradle from your machine.
   ```bash
       gradle build
    ```
10. Locate the .JAR file, which is stored in the build directory under the libs folder.
11. Navigate to the location of the .jar file and copy the file to the droplet.
    ```bash
       scp <location .jar> <destination on droplet>
    ```
    
12. Navigate to the root directory on the droplet and confirm that the file has been successfully uploaded.
    
    <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/JarFile%20available%20on%20%20Droplet.png?raw=true"/>
    
14. Since Java was already installed on the droplet (Step 7), you can execute the application.
    ```bash
       java -jar java-react-example.jar
    ```
    
    
15. Navigate to the **Networking** tab in the left menu, select Firewall, and click on the droplet's firewall.
    
    <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/SettingUpFirewall.png?raw=true"/>
    
16. Add a new rule that allows access on port 7071 from all IP addresses, as the app must be accessible to anyone.
    
    <img src="https://github.com/lala-la-flaca/deploy-java-app-digitalocean/blob/main/resources/Img/Allowing%20access%20to%20port%207071.png?raw=true"/>
    
18. Open a browser and use your droplet's IP address:port
    
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
3. Ensure to add the public SSH key to the .SSH directory of the new user.
4. Add the authorized_keys file and copy the public key of your machine.
5. Copy the file from the machine to the droplet  using the new user.
6. Execute the application.
   



    
 
     
  
























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
