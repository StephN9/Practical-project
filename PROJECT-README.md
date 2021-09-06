# Practical Project

<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/StephN9/Practical-project">
    <img src = "https://devopedia.org/images/article/54/7602.1513404277.png" alt="Logo" width="300" height="200">
</a>

  <h3 align="center">DevOps</h3>

  <p align="center">
    Group Project
    <br />
    <a href="https://github.com/StephN9/Practical-project"><strong>Explore the documentation »</strong></a>
    <br />
    <br />
    <a href="https://github.com/StephN9/Practical-project">View Demo</a>
    ·
    <a href="https://github.com/StephN9/Practical-project/issues">Report Bug</a>
    ·
    <a href="https://github.com/StephN9/Practical-project/issues">Request Feature</a>
  </p>
</p>



<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary><h2 style="display: inline-block">Table of Contents</h2></summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgements">Acknowledgements</a></li>
  </ol>
</details>



### Built With

* [AWS]()
* [Command Line]()
* [Docker]()
* [Jenkins]()
* [Git]()
* [Jira]()

###Brief

The brief for this project was to create a completed CI Pipeline with full documentation around the utilisation of the supporting tools. The requirements of the project are as follows:
•	A Jira board with full expansion on tasks needed to complete the project.
•	A record of any issues or risks that we face whilst creating our project.
•	The application has to be deployed using containerisation and orchestration tools.
•	The application has to be tested through the CI pipeline
•	There has to be a managed Database Server
•	If a change is made to the code base, Webhooks should be used so that Jenkins builds, tests and deploys the changed application.
•	The project must make use of a reverse proxy to make the application accessible to the user.

###Planning

The first thing that we did for our project was to create a list of features based on the brief and prioritise them using the MoSCoW methodologies. The features required for the minimum viable product were placed under the ‘Must have’ column. Then the remaining features were placed under the remaining three columns based on how difficult and time consuming they would be when compared to have much of a positive impact they would have on the end product.
 


We then focused on designing what we thought the AWS architecture should be based on the brief. We used DRAWIO.IO to create this diagram, as it has a built in AWS section which allowed us to easily identify AWS services for the diagram. When creating this diagram, we were focusing on the overall structure which the infrastructure should have, as well as the ideal CIDR range for the VPC and subnets, and which ports would need to be available in the security groups for the end product to work.
 
We also created a diagram for our CI pipeline to help illustrate which parts of the pipeline would be achieved by which programme.




###Project Management

In order to manage our project, we used Jira Software to create an Agile Scrum Board which is based online at Atlassian (link provided under resources). We used this to create tasks based on the specification given in the brief for the project. We also created Epics to group together the tasks which were focusing on a specific aspect of the project, we ended up having five Epics which the majority of our tasks fell under when applicable; these were GitHub, AWS Architecture, Jenkins, Docker and NGINX. Each of the tasks that we created were given a story point estimate which we used to help us judge how much work we had remaining on the project. We also implemented the use of prioritisation arrows to help us determine what priority each task had based on the MoSCoW prioritisation we had previously decided.





We used this Scrum Board throughout the project and created sprints for groups of tasks. This allowed us to easily see how we were progressing throughout the project, and what work we had remaining to complete and how complex the remaining tasks were.




Another area of project management that we focused on before starting to work on our project, was a risk assessment matrix. We created a list of risks which we thought could negatively impact the project. We also used this throughout the project and have been adding to it when it has become apparent that a risk might occur or needs to be mitigated. We identified 10 risks that our project could be susceptible to, and created a table for these risks. Within this table we identified the following for each risk; the risk, an evaluation of the risk, the likelihood and impact, as well as how is responsible for that risk, what would happen if the risk were to occur and what control measures, we had put in place for the risks.
 

 
###Version Control
We used GitHub as a Version Control System for this application, we created aa public repository which we cloned the project repository on to. We created a develop branch from the main branch, and then created feature branches based on which feature that current sprint was focusing on. This ensured that we maintain a working version of the code that we could go back to if we needed to.

 
Example of the network graph for our GitHub repository, and how we have utilised branches.
We added branch protection rules to our main branch as this would be the branch which would trigger a Jenkins build. These rules ensured that one other person would have to review the changes before the merge was allowed. 

 
Example of adding everyone on the project as a collaborator.

 
Example of the branch protection rule we created for the main branch.

 
Here is an example of one of our merge requests having to be reviewed and accepted by the other member of the team in order for the merge to take place.

###AWS Infrastructure
For the Cloud based infrastructure we used AWS services to create the environment. We used a VPC with a CIDR range of 172.10.0.0/16. We then had two subnets, subnet 1 had a CIDR range of 172.10.1.0/24, this subnet contained the three EC2 instances which were used for hosting the CI Server and Docker. Subnet 2 has a CIDR range of 172.10.2.0/24 and contained the AWS RDS database which was used as the database server. Each of these subnets had a different security group attached which has specific inbound rules set up to allow the throw of traffic through whilst also ensuring that they remain as secure as possible.
 
Example of our inbound rules for Subnet 1 which contained the EC2 instances.
We then also created an EC2 instance within subnet 2 (which hosts the RDS database). We then also created an Internet Gateway connected to the VPC which allowed incoming traffic on port 80, and created a NAT Gateway with a route table which pointed to subnet 2 and allowed internet access to the EC within subnet 2.

###CI Server
The CI server which we are running for our project is Jenkins. This is a free and opensource automation server, which runs on port 8080. The Jenkins server uses a Jenkinsfile at the base of the directory which has the stages that Jenkins will automate in the process. Our Jenkinsfile automates the building of the images, running both the front and backend tests, and deploying the containers. 

 
Here is the Jenkinsfile which we created and is stored on our manager EC2 instance.

 
Here is an example of how the project pipeline is displayed when a new build is triggered, it demonstrates which stage of the build has either passed or failed.
We have configured a webhook on our GitHub repository and on Jenkins which when the code is updated on the repository on the main branch it will trigger a new build on Jenkins. This will then automatically go through the build, test, and deploy stages stated within the Jenkinsfile. As illustrated above it will clearly indicate whether a build has succeeded or failed based on the new code which has been provided.
We have also amended our Jenkinsfile so that for each build that Jenkins creates the test results for both the front and backend tests are stored as artifacts. This allows us to go back to these test coverages at a later date, as they have been turned into artifacts for each build.

 
Here is an example of the backend and frontend tests being retained as artifacts which can be accessed at a later date.
In order for Jenkins to automate the CI pipeline it uses docker-compose to build the containers and docker stack to deploy the containers. However, both of these commands require Jenkins to have access to the docker-compose.yaml file in order for these commands to be automated. The docker-compose.yaml file contains both the database URI (which contains the database endpoint and password) and the secret key, both of these are variables which you don’t want available within your file structure for people to be see as they would be able to access the database. So, in order to prevent this we have the docker-compose.yaml file as a credential within Jenkins,  as this way Jenkins is able to access the file but it wouldn’t be stored anywhere within your code base, as the docker-compose.yaml file is stored locally and uploaded to Jenkins as a credential.

 
Example of docker-compose.yaml file being stored as a global credential on Jenkins.

 
Here is the docker-compose.yaml file we created for Jenkins to use within the stages, this is kept locally on a private PC and uploaded to Jenkins as a credential.
For each of the stages which require the docker-compose.yaml file Jenkins will copy the yaml file to a new docker-compose.yaml file, use it within the step that requires it, and then it will delete the copy which has been made within the same stage.
Docker-compose.yaml file as a credential

###Cloud Server
For this project we created three EC2 (Elastic Compute Cloud) instances on AWS for our docker containers to run on, two of these were t2.Medium and one was a t2. Small. AWS manage All of the EC2 instances which we created for this project run Ubuntu 18.04, and have docker and docker-compose installed on the machine. For the EC2 instances which are used for the docker swarm containerisation we have given them a security group which has the following inbound rules which limit the amount of access people have to these instances. 
 
To access these EC2 instances we created a specific pem keys for the project, there is one pem key which can be used to access the three instances which run docker swarm. Then there is a separate pem key which can be used to SSH into the instance within the same subnet as the RDS database.
AWS maintain the hardware and virtualisation of these EC2 instances, and only require the user to maintain and choose the operating system which is used on the instances. This means that because of the resources available to AWS that they have a high availability in case there is a malfunction which means the hardware for one of the instances isn’t working.

###Database Server
For the database server we used an Amazon Web Service RDS. This is a Platform as a Service option which they provide for hosting databases on the Cloud. It allows you to initially chose the hardware and software you want for your database, but then AWS manage and maintain the operating system, the virtualisation and the hardware for that database.

 
Example of our RDS database on AWS.
Containerisation and Orchestration
For our method of containerisation on our EC2 instances we used docker and docker-compose. We used docker to build the images for the containers which we required, we then pushed these up to docker-hub so that they were globally available.

 
Examples of the images we build for the project frontend application and then project backend. 
These images were then used on the docker-compose.yaml in order for docker swarm to be able to deploy the containers (and their replicas). We used docker-swarm on our three EC2 instances to ensure that if one instance went down that there would then be another one in place which would be able to take the load from the broken container whilst maintaining high availability for the user. We had once EC2 instance which was a manager for docker swarm and then had two worker nodes (the other two EC2 instances), these nodes created an overlay network which allowed the replicas created by the docker-compose.yaml to be spread across all three instances even though the IP addresses were separate.
 
Illustration of the docker swarm structure we created, and how these were used to containerise and orchestrate the different applications and servers.
We created three replicas for each of our containers as this ensures that there should be high availability for the application even if one of the EC2 instances goes down, or updates are being rolled out.


###Reverse Proxy
For our reverse proxy we used NGINX, this handles incoming traffic from the user and directs it towards the frontend applications using the nginx.conf file which we created. This means that people are able to access the webpage by using the public IP address of any of the EC2 instances, and then this will proxy pass them to the frontend application. It will then also forward any responses back to the client as well.

 
Here is the nginx.conf file within our AWS structure which is mounted onto the nginx:latest image when a new container is created by docker swarm.


###Continued Development
If we were to develop our project further, we would focus on:
•	Integrating the Blue Ocean Dashboard Plugin as it makes the interface more user friendly. It also has a has a more intuitive interface when a Jenkinsfile and build fails, so the user would be able to more easily see which aspect of the build wasn’t successful. 
•	We would also focus on creating a Multi-branch pipeline on Jenkins rather than a normal pipeline, as this would allow us to create builds from multiple branches of the Git Repository. This means that rather than having to amend the webhook when we wanted to build from a new branch, we would be able to build from multiple branches and have Jenkins categorise these based on the branch.



<!-- USAGE EXAMPLES -->
## Usage

This project was set up to demonstrate our understanding of and ability to:
* Host on AWS
* Use Command Line to install software and plugins
* Use Docker to separate infrastructure from the application, run it and ship updates
* Utilise Jenkins for automated building, testing and deploying updates continuosly
* Use Git to allow for branches and open source contribution
* Setup, manage and use Jira to document the planning, progress and amendments to the project

<!-- ROADMAP -->
## Roadmap

See the [open issues](https://github.com/github_Obscur4ns/catsProject/issues) for a list of proposed features (and known issues).



<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request for review



<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE` for more information.



<!-- CONTACT -->
## Contact

Daniel Hall - Github.com/Obscur4ns
<br> </br>
Stephanie Norman - Github.com/StephN9
<br> </br>
Project Link: [https://github.com/github_StephN9/Practical-project](https://github.com/github_StephN9/Practical-project)



<!-- ACKNOWLEDGEMENTS -->
## Acknowledgements

* Luke Benson - Teaching us the DevOps
* Stephanie - Collaborator
* Daniel - Collaborator



<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
[contributors-shield]: https://img.shields.io/github/contributors/github_StephN9/repo.svg?style=for-the-badge
[contributors-url]: https://github.com/github_StephN9/repo/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/github_StephN9/repo.svg?style=for-the-badge
[forks-url]: https://github.com/github_StephN9/repo/network/members
[stars-shield]: https://img.shields.io/github/stars/github_StephN9/repo.svg?style=for-the-badge
[stars-url]: https://github.com/github_StephN9/repo/stargazers
[issues-shield]: https://img.shields.io/github/issues/github_StephN9/repo.svg?style=for-the-badge
[issues-url]: https://github.com/github_StephN9/repo/issues
[license-shield]: https://img.shields.io/github/license/github_StephN9/repo.svg?style=for-the-badge
[license-url]: https://github.com/github_StephN9/repo/blob/master/LICENSE.txt
