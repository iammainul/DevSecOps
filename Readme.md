# Integration of Security in CICD

## What is CICD

CICD is a combination of two terms which you may have heard of. *CI = Continuous Integration* & *CD = Continuous Deployment*. In this fast moving agile development we want to get fast results of our code generated and perform task as soon as there are changes made. So, what we do we automate the process using certain tools which we will find out below.

What happens is we collect the code in a single repository and as soon as we integrate some new code with the previous code and commit in the repository a number of steps get triggered. Which then checks form code quality to deployment dependencies, and generates a report based on the result. Based on the results our build fails or gets successful and the changes get deployed.


## Our Purpose

Here we are using *CICD* to demonstrate the automation process of the security testing of the code. We will be covering both. *SAST = Static Application Security Testing* and *DAST = Dynamic Application Security Testing"*.

*This documentation will be focused towards Windows based CICD development as there are lots of documentation is available for Linux.*
We will be deploying a Java Application which we will pull from github and continue to use that source code throughout our development.



# Installation of Tools

## Jenkins

To install Jenkins it is recommended to download the latest version from this [link](https://jenkins.io/download/).

### Dependencies

It is recommended that all the Java and Tomcat dependencies are met.

## SonarQube

I have used the community version of SonarQube for this project.
Visit the SonarQube Website and download the latest version from this [link](https://www.sonarqube.org/downloads/)

To run SonarQube as a solo entity it is recommended to download the SonarRunner file from this [link](https://docs.sonarqube.org/display/SONARQUBE45/Installing+and+Configuring+SonarQube+Runner)

## Checkmarx

I had a Checkmarx license which I used for this project. More on that in the setup part.



# Setup

## Getting The CODE

First of all we go to Jenkins dashboard and create an freestyle project. After the project has been created we fill the necessary fields. Like Description and other options.
Next we move on to the source code management and select the preferred method. I am using github here with a public repository. If you have a private repository you can add credentials as well to connect.
![github](/Images/GetCode.jpg)
Git Setting in Manage Jenkins
![git](/Images/Git.jpg)

## SonarQube
 
First of all we need to setup SonarQube and SonarRunner. Please find the images to setup SonarQube and SonarRunner.
Then we go to Jenkins dashboard and create an freestyle project. We configure the source code management as we did in the last step.
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

![SonarQube](/Images/GobalSettings.jpg)


## Checkmarx

First of all we again go and fill up the Checkmarx Credentials details in the Manage Jenkins section. 
![CheckMarx-1](/Images/ManageJenkins_Checkmarx.jpg)
After that we create a freestyle project and after filling up the necessary details, we go and create a build step where we execute Checkmarx scan.
![CheckMarx-2](/Images/Checkmarx-2.jpg)
The details will get filled on its own. It's up to you how you want to play with it.

## Deployment

As my project was a MAVEN Project, i created a maven project from Jenkins Dashboard. Then After we add the pom.xml file and set goals and options as clean package to build it.
As a post-build action we Deploy the war/ear to  container.
![Deploy-1](/Images/Deploy-1.jpg)

## ZAP Proxy

Coming Soon
