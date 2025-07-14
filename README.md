# SDLC-Automation


 CI-CD : Continuous integration Continuous deployment.

 Difference between continuous deployment and continuous delivery 

 source code------>-------Test------>-------Build------>-------QA------>-------Release

- Continuous integration goes till **build**
- Continuous delivery from **build** to **QA** and then **stops**
- Deploy from **stop** to **release**
- Continuous deployment goes from **build** to **release** without stopping

> **Continuous Deployment:** an update is automated the whole way out to production without the safeguards of continuous delivery. 
> **Continuous delivery:** focus on safely getting changes out to production. Key point: there is a stop for approval before going to production.

# Developer Tools on AWS

Implement CICD with AWS dev tools to accelerate the software development and release cycle.

code commit -> code build -> code deploy.

We can manage and automate all this with **CodePipeline**.

----
----
# CodeCommit
It is a managed service that hosts private git repositories.

- Managed service like RDS, rds is a database where we have no concerns about whats going on behind the scenes.
- Same thing like codeCommit, we dont worry about the servers AWS manages the servers for us.

**Why not use Git ?** 
We can use git but the key term here is managed service, if we dont use codeCommit we have to take care of servers. Which AWS manages it for us.


## Benefit of CodeCommit

- Highly available, scalable, and fault tolerant.
- No size limit.
- Integrates with other aws services (codeBuild, CodePipeline, CodeDeploy, Lambda, SNS) these services are key tools for setting up automations.
- Works with existing git-based tools.


## Demo on creating a repository in aws management console.

- Search **CodeCommit** on AWS and create a repository.
- Look here for more Steps in detail: [Demo_CodeCommitActions.md](https://github.com/Ashutoshdikshit07/SDLC-Automation/blob/e671dab409b01aaad5991f8cadc7880b7742e569/Demo_CodeCommitActions.md) 


>there are other repositories that can be used in AWS deployments include S3, GitHub, BitBucket and github enterprise.


# CodeCommit Data Security

Create an IAM group to manage the developers in one place and attach that policy to the group.


----
----

# CodeBuild

Fully managed continuous integration service that compiles source code, runs tests, and produces software packages that are ready to deploy.
It is charged on how many operations we are doing, how long we are running and not on hardware.

> Here we dont have to maintain the servers that is done by AWS.

## How do we access CodeBuild ?
- Management Console
- CLI
- SDK
- CodePipeline

----

- We have a codeCommit from where we get the code
- we build it using CodeBuild where it is fully managed, No need to provision/scale servers, prepackaged build environments.
- We perform our build and need to store those outputs artifacts and we store them in S3. Here we need to turn on versioning, encryption.
- This then goes to CodeDeploy.

Here we see the making of our pipeline.

 **How can CodeBuild be used ?**

- It can be added to the build stage and also the test stage in a pipeline.
- You must provide CodeBuild with a **build project**.
- **What is a build Project ?**
   -  Build Project includes information about how to run a build, including where to get the source code, which build environment to use, which build commands to run, and where to store the build output.
  

## How does CodeBuild Work ?

1. We need to provide **CodeBuild** with a build project, and build project is going to tell **CodeBuild** how to perform the build.
2. **CodeBuild** uses **BuildProject** to create a build environment.
3. There is a source code which downloads in the build environment and uses build specification known as **buildspec** file.
    - **buildspec** file is a collection of build commands and related setting that **CodeBuild** uses to run a build
4.  CodeBuild sends the output of a build to our output repository S3, other things it can do is setup notifications so can involve **SNS** here (follow demo- [DEMO-CodeCommit-TriggersEmailNotifcation.md](https://github.com/Ashutoshdikshit07/SDLC-Automation/blob/fbcc6d7af1d40c018c00b127a01404b6bd69c530/DEMO-CodeCommit-TriggersEmailNotifcation.md) )
5. While our build is running it can do 2 things.
   - build Project can send information to CloudWatch
   - Information can be send to CodeBuild
6. While our build is running, we can use our interface of choice (CLI, Management console, SDK, CodePipeline) to get updates on our build
   - We can do that from CloudWatch or look and CodeBuild from these interfaces. (we can see all these once we go into CodePipeline

- In S3, we need an input bucket and output bucket.
  - our input is comming from CodeCommit. We output it to S3.
  - That output will be the input for the next stage, CodeDeploy or the deployment stage to be specific. Here we can also use Jenkins with AWS plugin for our deployments.
  > we need our buckets versioned, and these buckets should be in the same region as our build.

## use cases

We can set up cloudWatch events to monitor our repository and after successful commit to the repository, we can trigger the CodeBuild to run a code on that just merged source code. We can even have a lambda function to trigger on an update to codeCommit or merge.

> EventBridge and cloudWatch is the same thing.


## Do we need a build Stage ? 
Only if our code needs to be built or packaged. 
Eg. For Java, you build JAR file, whereas for HTML does not need a build.


# Build Projects and Buildspec file

From Source code we create a build Project, **build Project** creates a build environment but we need a buildspec file

## Steps in a Build Project

1. Our Project is submitted.
2. Provisioning starts, Provisioning means what ? CodeBuild is a managed service so we are not thinking of servers but we need build servers. (AWS is handling that for us)
3. Download source code (typicalling our **buildspec** file is zipped with the source code)
4. It installs.
5. Pre-build phase (get into details once we understand more about buildspec file- YAML format)
6. then build phase
7. post build 
8. Artifacts (this is what we get after post build phase)
9. Finalizing
10. Completing
11. Built output artifact is going into S3(lets say Jar file)
12. Then goes into codeDeploy

## Buildspec
It is a collection of build commands and related settings, in YAML format, that codeBuild uses to run a build.

### How does a buildspec file work with the build environment ?
- Include as part of source code.
- Or define a buildspec when you create a build project.

### Benefits of using buildspec ? 

Without buildspec, **CodeBuild** cannot successfully convert your build input into build output or locate the build output artifact in the build environment to upload to your output bucket.

> [!TIP]
> 1. if we include buildspec as part of the source code, by default it should be named as **buildspec.yml** and placed in root of your source directory.
> 2. we can specficy only 1 buildspec for a build project, regardless of the buildspec file's name.


## Running CodeBuild Locally 

It helps us to test our buldspec file before running.

1. Install git on local machine
2. install and set up Docker on local machine
3. Set up the build image - you can pull it from the CodeBuild public amazon ECR repository
4. Download the CodeBuild Agent
5. Run the CodeBuild Agent.

## CodeBuild with VPC - DEMO

CodeBuild cant access resources in a VPC, but we can enable this

**USECASES**
1. Run integration tests from your build against the data in an Amazon RDS database thats isolated on private subnet.
2. Query data in an amazon ElastiCache cluster directly from test.
3. Interact with internal web services hosted on Amazon EC2, Amazon ECS, or services that use internal **Elastic Load Balancing**


## DEMO - CodeBuild with VPC
1. Make sure you have a **codeCommit Repo** before starting with **CodeBuild**.
2. Create a CodeBuild Project, Use below image for reference.
   <img width="802" height="915" alt="Screenshot 2025-07-14 at 12 36 53 PM" src="https://github.com/user-attachments/assets/8edca0fd-874d-4809-952a-55bca02adc2f" />

3. Make sure you have a VPC created with private and public subnet setup with internet gateway and NAT - if not follow the documentation : [README.md] (https://github.com/Ashutoshdikshit07/SecureScalableAWSDeployment/blob/bcdd932baf86020f773c9e29aa53b33cce2e7d26/README.md)
4. Look for additional configuration and select VPC and subnet that you just created and validate it- Refer below screenshot.
    <img width="890" height="808" alt="Screenshot 2025-07-14 at 1 13 49 PM" src="https://github.com/user-attachments/assets/957fdd3c-a544-4213-be9b-7a99571f9e82" />
5. Create build project. Now our build project can access resource within that VPC.



