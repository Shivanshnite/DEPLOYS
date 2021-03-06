# HOME WORK SUMMARY

Assuming that git,docker and Jenkins are installed in the user respective system.

In this project there are two environment created using docker


1.TESTING ENVIRONMENT(USER CAN TEST THE PROJECT BEFORE COMMITING INTO PRODUCTION ENVIRONMENT)
2.PRODUCTION ENVIRONMENT(AS THIS IS A PRODUCTION ENVIRONMENT, SO ONLY SUCCESSFULLY BUILD PROJECT AND VERIFIED BUILD IS ALLOWE

For making this AUTOMATED(END-END) we are using jenkins

## IN GIT HUB REPO :

![NEW REPOSITORY](https://github.com/Shivanshnite/DEPLOYS/blob/master/new%20repository.png)

Consider there are two branches master and deploy according to my repository and whatever happen in the master is showed in Production Environment and changes made in deploy is shown in Testing Environment

## IN GIT BASH:

Supposing user has created two branches in git bash and using remote linked to the origin account github/user_name/user_content/branch_name/.com 
supposing user commit and pushed into github
![Git Bash](https://github.com/Shivanshnite/DEPLOYS/blob/master/git%20bash.png)

### STEPS TO MAKE END TO END AUTOMATE:

PreRequisite:
Server OS(REHL8/etc)
install httpd
Run httpd command (systemctl start httpd) 
docker should be installed
GIT Bash
In RHEL8.0 Firewall should be stop (systemctl stop firewalld)



## 1.CREATE GIT REPOSITORY
SEE THE IMAGES FOR A GENERAL IDEA
![NEW REPOSITORY](https://github.com/Shivanshnite/DEPLOYS/blob/master/new%20repository.png)
![branch_change](https://github.com/Shivanshnite/DEPLOYS/blob/master/Branch.jpg)


## 2.GIVING JENKINS POWER TO RUN COMMAND ON REDHAT LINUX 8

  Editing the file *sudoers* in your RHEL8.0
  
  
## 3.TUNNELING

  For tunneling I'm using ngrok you can use this application or similar application in RHEL8
 `*./ngrok https 8080*` this command will help to run a tunnel which will help to connect the jenkins to outside world.
 ![ngrok](https://github.com/Shivanshnite/DEPLOYS/blob/master/ngrok.PNG)
 
## 4.WEBHOOK
  In your repository there is an option of settings go to Settings/Webhooks and add webhook there 
  For adding webhook use the tunneling ip which was provided by ngrok:
                  `https://ngrok_ip/github-webhook/`
  
## 5.creating the production job in jenkins

   ![JOB_create](https://github.com/Shivanshnite/DEPLOYS/blob/master/job_create.PNG)
   
   Create a job and go to configure of your job and fill the data provided in image and give url of your *Git repository/master branch* in SCM and select the branch master.
    Next go to BUILD TRIGGER and tick this option GitHub hook trigger for GITScm polling to trigger automatically
    
   ![configure](https://github.com/Shivanshnite/DEPLOYS/blob/master/configure.png)
    
    
    IN EXECUTE SHELL FOLLOW THESE COMMANDS PROVIDED IN IMAGE
   ![JOB2_1](https://github.com/Shivanshnite/DEPLOYS/blob/master/Job2_1.png)
   ![JOB2_2](https://github.com/Shivanshnite/DEPLOYS/blob/master/job2_2.png)
   ![JOB2_3](https://github.com/Shivanshnite/DEPLOYS/blob/master/job2_3.png)
    
    

## 6.Creating the developer Job in Jenkins

  ![JOB_create](https://github.com/Shivanshnite/DEPLOYS/blob/master/job_create.PNG)
  
  ![configure](https://github.com/Shivanshnite/DEPLOYS/blob/master/configure.png)
  
  Same as Production Job only there is a difference is select the branch to deploy
  Remote trigger in Build trigger because with this we can trigger this job remotely and as soon as we push this job will run automatically.
  
  ![JOB1](https://github.com/Shivanshnite/DEPLOYS/blob/master/job1_1.png)
  ![JOB1](![JOB1](https://github.com/Shivanshnite/DEPLOYS/blob/master/job1_2.png)
  ![JOB1](![JOB1](https://github.com/Shivanshnite/DEPLOYS/blob/master/job1_3.png)
  
  
## 7.MERGING JOB in jenkins
  
  ![JOB_create](https://github.com/Shivanshnite/DEPLOYS/blob/master/job_create.PNG)
  
  CONFIGURE: 
  
  ![configure](https://github.com/Shivanshnite/DEPLOYS/blob/master/configure.png)
  
  Again create a job in jenkins and in git url provide a url of master branch because it is our production system.
  If and only if testing build/Developer build successfully runs.
  This concept is known as chaining as soon as developer build job will run successfully this build will start automatically
  In this build we will merge the content of the deploy branch with master.
  
  Provide these commands in your configure section 
  
  ## IN EXECUTE SHELL FOLLOW THESE COMMANDS PROVIDED IN IMAGE
   
  ![Job3_1](https://github.com/Shivanshnite/DEPLOYS/blob/master/Job3_1.png)
  
  ![Job3_2](https://github.com/Shivanshnite/DEPLOYS/blob/master/job3_2.png)
  
  ![Job3_3](https://github.com/Shivanshnite/DEPLOYS/blob/master/job3_3.png)
  
  ![Job3_4](https://github.com/Shivanshnite/DEPLOYS/blob/master/job3_4.png)
  
  
