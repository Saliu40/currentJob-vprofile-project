The Name of this Project is continuos integration on AWS: Using AWS services for CICD
# Services Used:
1 BitBucket for source code
2 AWS Code Artifact for Maven Dependencies 
3 AWS Code Buuild to build Artifact
4 Sonar Cloud for Code Analysis
5 AWS S3 Bucket for Storage
6 AWS SNS for Notification
7 AWS code pipeline
<img width="903" height="470" alt="Screenshot 2025-10-22 110158" src="https://github.com/user-attachments/assets/4583cf74-3ee9-4471-9344-16b2acaaab14" />

#This Project Architectural Diagram
<img width="1887" height="897" alt="Screenshot 2025-09-09 114828" src="https://github.com/user-attachments/assets/107b0915-c4ad-4d4f-b8f1-88a185921f1d" />

we clone the source codes to our local repositories  (https://github.com/Saliu40/currentJob-vprofile-project.git)
we can use anycode editor for code changes, but on this project, we used Visual Studio Code.

STEP1:
<img width="930" height="139" alt="Screenshot 2025-10-22 112338" src="https://github.com/user-attachments/assets/c763471a-10a9-4eca-96f5-fe05189c7b6f" />

<img width="728" height="685" alt="Screenshot 2025-09-09 123013" src="https://github.com/user-attachments/assets/694cd18e-a7bf-4eba-91fe-a47edfb8ed05" />
<img width="950" height="644" alt="Screenshot 2025-09-09 123422" src="https://github.com/user-attachments/assets/46a993e2-c9e1-4e5c-8565-867da5dbee5d" />
<img width="950" height="780" alt="Screenshot 2025-09-09 123536" src="https://github.com/user-attachments/assets/70abe32d-58f2-4e2f-941e-c2b257186cf9" />
After creating a remote workspace, $ repo on Bitbucket, for SSH Authentications, we copy our local public_key to add it on our bitbucket SSH-keys under settings. 
Test the Connection.
<img width="927" height="356" alt="Screenshot 2025-09-09 124855" src="https://github.com/user-attachments/assets/6da88ace-d767-4348-b9fe-20311f54ab9f" />

Migrating source Code to Bitbucket:
1. Clone The source Code to Ur Local Repo(git clone https://github.com/Saliu40/currentJob-vprofile-project.git)
2. cd into into the project
3. Remove the Remote Origin:
   before that we need to checkout to all the branches
   this for loops comand will list all branches and check all out instead of doing it individually. we just automate it using for loops command: for i in git branch -a | grep remotes | grep -v HEAD | grep -v master | cut -d / -f3; do git checkout $i;done
   after that we remove the remote Origin (git remote rm origin).
   <img width="907" height="320" alt="Screenshot 2025-09-09 131219" src="https://github.com/user-attachments/assets/976b2c4f-0235-4dac-bb07-ef922344f0cf" />

5. add the new Bitbucket remote URL:
   copy Ur remote repo URL
<img width="1017" height="714" alt="Screenshot 2025-09-09 131406" src="https://github.com/user-attachments/assets/ea930dd3-692b-483b-9ceb-64cc509a4536" />
Git remote add origin repo URL &
Git Push origin --all (to push Ur source code to the new remoe repo created on bitbucket)
<img width="680" height="889" alt="Screenshot 2025-09-09 131814" src="https://github.com/user-attachments/assets/d177f848-f0b7-4e79-8dde-92f4851b4725" />

STEP2
<img width="856" height="167" alt="Screenshot 2025-10-22 112349" src="https://github.com/user-attachments/assets/f3f59a95-34f1-40f9-8cca-5566a15c79f5" />
1. Setting Up AWS Code Artifact Repository
create AWS free tier account if U dont have, if U already have, log into your AWS console, go to search and type code artifact.<img width="951" height="990" alt="Screenshot 2025-10-17 140303" src="https://github.com/user-attachments/assets/3d62ed01-e27b-4ea2-9203-c84196465f02" />


 
