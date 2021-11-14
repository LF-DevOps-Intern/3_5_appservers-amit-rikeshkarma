# GlassFish Task Solution:

1. Install GlassFish server and change HTTP port to 8088.

### Install GlassFish
  - Install JDK at first
    - `sudo apt install openjdk-11-hre-headless`
  - Download the zip file for GlassFish 6.2.2 from github link
    - `wget https://github.com/eclipse-ee4j/glassfish/releases/download/6.2.2/glassfish-6.2.2.zip`
  - Once its downloaded, extract using following command
    - `unzip glassfish-6.2.2.zip`
  - Now we get the directory called glassfish6 inside glassfish-6.2.2.
  - Then we can navigate to glassfish4/bin and run the following command to start the server:
    - `./asadmin start-domain`
  - Our server has now been started.
  
## Change HTTP port to 8088
  - Run the GlassFish server and connect to the administrative interface using the default port (4848)
  - In the left menu go to **Configurations**
  - Then select **server-config**
  - Now go to **Network Listeners** 
  - Select **http-listener-1** and change its port value to **8088**
  - Click save and restart the server  
  ![Network listeners](https://github.com/LF-DevOps-Intern/3_5_appservers-amit-rikeshkarma/blob/main/Glassfish/snapshots/change%20port%20to%208088.png)  
  ![Port: 8088](https://github.com/LF-DevOps-Intern/3_5_appservers-amit-rikeshkarma/blob/main/Glassfish/snapshots/server%20started%20at%20port%208088.png)

1. Create a demo Java (11) servlet application with maven.
   - Install Intellij IDEA and Create a new Maven Project      
    ![Create new maven project](https://github.com/LF-DevOps-Intern/3_5_appservers-amit-rikeshkarma/blob/main/Glassfish/snapshots/create%20maven%20project%20in%20Intellij.png)
   - Using pom.xml to manage the project dependencies
     - POM stands for “Project Object Model”. It is an XML representation of a Maven project held in a file named pom.xml.
       - Here we need to add the servlet dependencies in order to work with it.    
    ![Adding Dependencies](https://github.com/LF-DevOps-Intern/3_5_appservers-amit-rikeshkarma/blob/main/Glassfish/snapshots/adding%20dependency%20code%20on%20pomxml.png)
   - Create a new folder named java inside src/main folder, then set the java folder to sources root so as to show ‘Class’ on the IntelliJ IDEA when we right-click and select ‘New’.
   - Create a new class inside the java folder named DemoServlet.java inside the demo folder.     
    ![Project Setup](https://github.com/LF-DevOps-Intern/3_5_appservers-amit-rikeshkarma/blob/main/Glassfish/snapshots/project%20setup.png)
    
2. Generate war package.
   - To generate a war package we need to run the following command inside the project directory:
     - `maven package`
   - The demo_project.war file is generated inside ~/demo_projects/target.      
    ![War package generate](https://github.com/LF-DevOps-Intern/3_5_appservers-amit-rikeshkarma/blob/main/Glassfish/snapshots/war%20package%20generated.png)
    
3. Deploy the war using glassfish app server.
   - Deploy the war using the glassfish app server.
       - To deploy we need to start the GlassFish server first by navigating inside glassfish4/bin like before and run the following command to start the server:
         - `./asadmin start-domain`
         - Then we need to run the following command to deploy the war file we just generated:
           - `./asadmin deploy /home/rikeshkarma/IdeaProjects/demo_project/target/demo_project.war`     
    ![Deploy war package](https://github.com/LF-DevOps-Intern/3_5_appservers-amit-rikeshkarma/blob/main/Glassfish/snapshots/deploy%20war%20file.png)         
    ![Deployed page](https://github.com/LF-DevOps-Intern/3_5_appservers-amit-rikeshkarma/blob/main/Glassfish/snapshots/deployed.png)