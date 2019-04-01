**Intregration of Security in CICD**

*This is focused towards windows CICD development as there are a lot available for Linux.*
We will be deploying a Java Application which we will pull from github and continue to use that source code throughout our development.



#Installation of Tools

##Jenkins

To install jenkins it is recommended to download the latest version from this [link](https://jenkins.io/download/).

###Dependencies

It is recommended that all the Java and Tomcat dependencies are met.

##SonarQube

I have used the community version of SonarQube for this project.
Visit the SonarQube Website and download the latest version from this [link](https://www.sonarqube.org/downloads/)

To run SonarQube as a solo entity it is recommended to download the SonarRunner file from this [link](https://docs.sonarqube.org/display/SONARQUBE45/Installing+and+Configuring+SonarQube+Runner)

##Checkmarx

I had a Checkmarx license which I used for this project. More on that in the setup part.



#Setup

##Getting The CODE

First of all we go to jenkins dashboard and create an freestyle project. After the project has been created we fill the necessary fields. Like Description and other options.
Next we move on to the source code management and select the preferred method. I am using github here with a public repository. If you have a private repository you can add credentials as well to connect.
![github](/Images/GetCode.jpg)
Git Setting in Manage Jenkins
![git](/Images/Git.jpg)

##SonarQube
 
First of all we need to setup SonarQube and SonarRunner. Please find the images to setup SonarQube and SonarRunner.
Then we go to jenkins dashboard and create an freestyle project. We configure the source code management as we did in the last step.
Now we add a build step: Execute SonarQube Scanner. Where we need to pit the Analysis Properties as per y project. I will give you an example.

``` SonarQube
#required metadata
sonar.projectKey=Demo
sonar.projectName=Demo
sonar.projectVersion=1.0
#path to source
sonar.sources=.
sonar.java.binaries=.
```
If you don't put properties your build will fail.

![SonarQube](/Images/GlobalSettigs.jpg)


##Checkmarx

First of all we again go and fill up the Checkmarx Credentials details in the Manage Jenkins section. 
![CheckMarx-1](/Images/ManageJenkins_Checkmarx.jpg)
After that we create a freestyle project and after filling up the necessary details, we go and create a build step where we execute checkmarx scan.
![CheckMarx-2](/Images/CheckMarx-2.jpg)
The deatils will get filled on its own. It's upto you how you want to play with it.

##Deployement

As my project was a MAVEN Project, i created a maven project from Jenkins Dashboard. Then After we add the pom.xml file and set goals and options as clean package to build it.
As a post-build action we Deploy the war/ear to  container.
![Deploy-1](/Images/Deploy-1.jpg)

##ZAP Proxy
