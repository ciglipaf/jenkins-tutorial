# Jenkins Tutorial
Jenkins is a continuous integration(CI) software. It is widely used for build and test projects continuously and integrate the changes. It is center of the builds for a developer team. In this tutorial we are going to use Jenkins CI with Github repository using Webhooks to notify Jenkins server. Also we will show you how to set up Jenkins locally using **Tomcat** and how to tunnel your localhost using **ngrok** so Github Webhooks can interact with your localhost like a server and push changes to the Jenkins server.

## Continuous Integration?
We have a developer team. They each code a few new classes and tested them well. But when they integrate their classes together bugs arise and code breaks. This problem is called an **integration hell**. Realizing this problem may be too late if the project schedule is near to the end as well as it will be expensive. To solve this problem, people get inspired from eXtreme Programming(XP).
The idea is simple. Instead of waiting lost of components to integrate, project is build whenever a developer pushes a new change to repository. So it will automatically build test and report each changes.

## How it actually works?
1. Developers push new code.
2. Repository (Github in this tutorial) changes.
3. CI server (local Jenkins in this tutorial) get notification either by Poll or Webhooks.
   **Poll**
CI server checks the repository regularly. It scans entire repository and verify it with the server. It is more expensive method than webhooks.
  **Webhooks**
> Webhooks allow external services to be notified when certain events happen within your repository.

is defined by Github Webhooks. When the repository changes, Github will POST the changes to our serever by adding server link to our Github settings. This will be explained soon in this tutorial.
4. If project build or test fails CI server sends notifications to team (e.g. by e-mail).
5. CI server generates reports.

### Download Tomcat
*If you don't want to host your jenkins in Tomcat, skip those steps and keep reading [here] (#use-jenkins-in-built-in-jetty-servlet)*

1. I have used latest tomcat version for now which is 9. Go [here](http://tomcat.apache.org/download-90.cgi) chose **Core** and select appropriate version for your system, i have chose **tar.gz** for my **OS X EL Capitan**
2. Extract it to somewhere that you have access, my tomcat location now is **/Users/cemalonder/Development/Libraries/apache-tomcat-9.0.0.M8**

### Download Jenkins
1. Go [here](https://jenkins.io/) and click on **Downlads** dropdown on the upper left, choose **2.9.war** file (or latest version at the time you are reading this tutorial).
2. Move **jenkins.war** file **webapps** folder which is under the tomcat path in the previous step. So my jenkins location is **/Users/cemalonder/Development/Libraries/apache-tomcat-9.0.0.M8/webapps/jenkins.war**

### Startup server
1. **cd** into your tomcat/bin path. Mine is **/Users/cemalonder/Development/Libraries/apache-tomcat-9.0.0.M8/bin**
2. type
> ./startup.sh

3. Now go to your **localhost:8080/jenkins** in your browser. Jenkins is running!
4. to stop tomcat, type
> ./shutdown.sh

### Use jenkins in built in Jetty servlet
Jenkins has built in **Jetty** servlet container. **cd** (change directory in terminal) into to your jenkins.war folder and type:
    java -jar jenkins.war
Now go to your **localhost:8080** in your browser. Jenkins is running!

## Build Triggers
- `Build when a change is pushed to Github`option is checked.
- Since jenkins is working on localhost, previous option is not worked. Github can't connect our localhost directly. So we used **ngrok** to create tunnel.


Now we are trying to push our repository to Github when we build our repository in Jenkins.
## Post-build Actions
- **Add post-build action** drop box is clicked.
- **Git Publisher** option is selected.
- **Push Only If Build Succeeds** option is selected.
- **Branch to push** option is filled by *master*
- **Target remote name** option is filled by *origin*

## Branches to Build
- **Branch Specifier** is left blank for jenkins to track all branches.

## How to merge branches that successfully build and push to remote master via Jenkins?
- [Here] is a good article.

[Here]: https://www.cloudbees.com/blog/dont-phunk-my-stable-branch-jenkins-pre-tested-commits-stop-breaking-stable-branches "Pre-tested commits"
