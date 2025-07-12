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
- Look here for more Steps in detail: Demo_CodeCommitActions.md 


>there are other repositories that can be used in AWS deployments include S3, GitHub, BitBucket and github enterprise.


