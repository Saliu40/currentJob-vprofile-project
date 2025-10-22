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

STEPS:
<img width="930" height="139" alt="Screenshot 2025-10-22 112338" src="https://github.com/user-attachments/assets/c763471a-10a9-4eca-96f5-fe05189c7b6f" />

<img width="728" height="685" alt="Screenshot 2025-09-09 123013" src="https://github.com/user-attachments/assets/694cd18e-a7bf-4eba-91fe-a47edfb8ed05" />
<img width="950" height="644" alt="Screenshot 2025-09-09 123422" src="https://github.com/user-attachments/assets/46a993e2-c9e1-4e5c-8565-867da5dbee5d" />
<img width="950" height="780" alt="Screenshot 2025-09-09 123536" src="https://github.com/user-attachments/assets/70abe32d-58f2-4e2f-941e-c2b257186cf9" />
After creating a remote repo on Bitbucket, for SSH Authentications, we copy our local public_key to add it on our bitbucket SSH-keys. 
Test the Connection.
<img width="927" height="356" alt="Screenshot 2025-09-09 124855" src="https://github.com/user-attachments/assets/6da88ace-d767-4348-b9fe-20311f54ab9f" />

Migrating Code to Bitbucket:
1. Clone The Code to Ur Local Repo(git clone https://github.com/Saliu40/currentJob-vprofile-project.git)
