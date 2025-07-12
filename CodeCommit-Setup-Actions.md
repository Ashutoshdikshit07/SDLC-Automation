# Create a Repository

Search CodeCommit on AWS and create a repository.

# Create an access key to use command line.

1. Before we do anything we need to be authenticated.
2.  Go to IAM
  - Users
  - select an user
  - Security credential tab
  - And here we need some access keys
    - Create access key and download it.
    - When not using the access keys dont leave it hanging and delete it.
   
3. Once access key is created we have to we have to work from command line.
  - Use cloudshell - Type it in search bar and get to cloudshell
  - enter command
    ```
    aws configure
    ```
  - Enter the access key id and the sercret access key into the console a
  <img width="1693" height="376" alt="Screenshot 2025-07-12 at 4 08 21 PM" src="https://github.com/user-attachments/assets/3284200d-47b3-468d-91d9-348234565125" />


# CodeCommit Commands to execute in CLI

1. Now we can start issues commands using cli to our account and specifically **codecommit**
  - Enter command -
    ```
    aws codecommit list-repositories
    ```
<img width="709" height="683" alt="Screenshot 2025-07-12 at 4 12 05 PM" src="https://github.com/user-attachments/assets/4d84fdcb-9c15-4d44-8f72-7b4bfe5e9a3d" />

2. Commands -
   ```
   aws codecommit create-repository --repository-name DummyR
   aws codecommit delete-repository --repository-name DummyR
   ```


# Some main GIT Commands - Cloning, Commit, Pushes, Pulls

```
git clone {link} local

git status

git add .

git commit -m "testing commit"

git remote (tells which branch we are working from)

git branch

git diff origin/main

git push origin main (what are we pushing? origin. Where are we pushing? main)

```

# CodeCommit Merging and Branching

```

git checkout -b newBranch

touch canary.json {write anything - file edited by one person} 

git add .

git commit -m "canary file added"

git checkout main

git merge newBranch


```
