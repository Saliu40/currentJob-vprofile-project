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
a. Setting Up AWS Code Artifact Repository
create AWS free tier account if U dont have, if U already have, log into your AWS console, go to search and type code artifact and create a repo.<img width="951" height="990" alt="Screenshot 2025-10-17 140303" src="https://github.com/user-attachments/assets/3d62ed01-e27b-4ea2-9203-c84196465f02" />
Get to know how it wolrks <img width="956" height="703" alt="Screenshot 2025-10-17 142122" src="https://github.com/user-attachments/assets/36a9ea24-4dff-45eb-b291-1a51c510e8d5" />

click on create and give it a name, select maven, thats where code artifact is going to get its depenencies from. <img width="939" height="868" alt="Screenshot 2025-10-17 142413" src="https://github.com/user-attachments/assets/f4b3a06c-f2ce-46cd-b9b1-eed48654c6d4" /> click on next
<img width="957" height="914" alt="Screenshot 2025-10-17 142938" src="https://github.com/user-attachments/assets/ba00eb46-45d4-410d-80bc-c76a4309ce5e" /> domain name should be included, create one if U dont have. click on next
create Ur repository <img width="946" height="956" alt="Screenshot 2025-10-17 143212" src="https://github.com/user-attachments/assets/2aa5cf4a-a2c3-4301-a02d-ad24d5ba82e5" />
<img width="923" height="966" alt="Screenshot 2025-10-17 143608" src="https://github.com/user-attachments/assets/2a3a95c8-af50-43d0-b06b-82f5dd876f74" />
<img width="920" height="758" alt="Screenshot 2025-10-17 143713" src="https://github.com/user-attachments/assets/893aff04-4aa0-4851-a18e-37ce0d3bfe52" />
Click on the maven-central-store to view connection instructions as we are going to use those autentications on our source code pom, & setttings.xml files <img width="961" height="1032" alt="Screenshot 2025-10-17 143857" src="https://github.com/user-attachments/assets/d5840f58-7fa7-4d54-8fd4-1412f28b36e9" /> select mac&Linux, or Windows depending on the Operating system using for the project.
b. going through pom.xml, settings.xml files of our prolject source code
use anycode editor to open the project repo, in my case am using a Vscode editor, <img width="942" height="927" alt="Screenshot 2025-10-17 145739" src="https://github.com/user-attachments/assets/f7163593-b680-4ec3-a685-86333d035c2d" />
Click on the Branches and select ci-aws (thats our current project Branch) <img width="923" height="1078" alt="Screenshot 2025-10-17 150139" src="https://github.com/user-attachments/assets/ded74a72-d266-4958-a9ab-1028ea5d8e30" />
<img width="932" height="768" alt="Screenshot 2025-10-17 150340" src="https://github.com/user-attachments/assets/db1bfd54-57eb-4ae0-9866-b4eaf9b4ba8b" /> thats our project source codes.
the buildspec.yml file represents code artifact file, it works like jenkinsfile, it is define using yml language

**##Setting Up Our Project Pom.xml, & Settings.xml Files##**
go to codeArtifact, select Maven-central-store, click on 'view connection introductions' select Ur Operating system, select maven on the package manager, and copy this URL

<img width="946" height="922" alt="Screenshot 2025-10-20 114226" src="https://github.com/user-attachments/assets/74c91595-e92c-48f5-99a8-794ed05346de" />
make sure to copy that Properly with no extral lines.

Use any editor, go to Ur Project Pom.xml file (make sure Ure in ci-aws Branch), scroll down to line 303 and change the Url to the Url copied from CodeArtifact>maven-centeral-store

<img width="916" height="837" alt="Screenshot 2025-10-20 114450" src="https://github.com/user-attachments/assets/4eaee7a9-b8af-4f43-b428-442d0dfec7c2" />

save the file and lets move to settings.xml file
paste the same Url on line 18, and line 30 on Ur settings.xml file

<img width="936" height="935" alt="Screenshot 2025-10-20 114824" src="https://github.com/user-attachments/assets/46b79cea-9085-4c49-be6b-e205afe4b6ec" />
Save and exit the file

Once Ure through, we go to the 'aws-files' a folder on the same repo, move the 'buildspec.yml file' to the root directory.

<img width="955" height="742" alt="Screenshot 2025-10-20 115006" src="https://github.com/user-attachments/assets/f685d090-0790-4faf-8e91-0f15254e1a6d" />
make sure those variable names U have here, match with your parameter store.
on line 15, the CodeArtifact authentication line, we will change that with our latest recently created codeArtifact Authentication  
go back to same codeArtifact>maven-central-store, click on 'view connection intrudction', select Ur OS, select maven as the package manager, and copy the codeArtifact Authorization for authentication.

<img width="932" height="717" alt="Screenshot 2025-10-20 115231" src="https://github.com/user-attachments/assets/d9fe2df3-8711-4680-8d3c-f6eb4b2e134c" />
paste the code on line 15 and save it, commit and push the changes to Ur BitBuckets repository
<img width="961" height="743" alt="Screenshot 2025-10-20 115431" src="https://github.com/user-attachments/assets/ba50f33a-755b-48b0-94f3-7382f69f171f" /> 
note that this buildspec.yml file works like our jenkinsFile, we define series of instructions we want our code build to achieve.
<img width="943" height="1007" alt="Screenshot 2025-10-20 120937" src="https://github.com/user-attachments/assets/c62bc597-3512-47c9-ac36-01fda1229235" />
changes made are saved on the Bitbukets repo

Setting Up our sonar Cloud, first loginto Ur github account on a browser, and go to sonarcloud.io
choose log in with github. <img width="956" height="910" alt="Screenshot 2025-10-17 152442" src="https://github.com/user-attachments/assets/222661d9-ab14-4e4a-9a68-d5c828348ef0" />
 It will loged you in using Ur github credencials.

Create a token on the sonarcloud, click on my Account, security and create a token
 save the token on Ur note pad
<img width="958" height="1021" alt="Screenshot 2025-10-17 152841" src="https://github.com/user-attachments/assets/97d32dbe-8321-406f-80a1-d8fc348d5cd2" />
Create New Organization by clicking the plus button <img width="1460" height="985" alt="Screenshot 2025-10-17 153328" src="https://github.com/user-attachments/assets/cfebc125-bfe4-4509-b486-944d8cad866d" /> Scroll down to select the free plan, and create the organization.

click on sonar cloud, click on Analze new project, U'll see an option to create a project manually 
and make sure U select the recent organization U just created on the organization drop down 
select public on the project visibility.
<img width="957" height="919" alt="Screenshot 2025-10-17 153722" src="https://github.com/user-attachments/assets/470bcaa2-c64d-4978-bef1-b84900e85817" />
select the previous version, & create the project
<img width="952" height="943" alt="Screenshot 2025-10-17 161426" src="https://github.com/user-attachments/assets/db11c10f-9b42-4928-9381-455d9b2dadf5" />
Click on the recently created project Information section to copy both the project key, & the Organization key, save them on Ur notepad<img width="945" height="892" alt="Screenshot 2025-10-17 161856" src="https://github.com/user-attachments/assets/f0424606-5ddd-441a-b2e9-5b7752d8121c" />

Stage5. Code Build Job: Creating a code build job is more like creating a Jenkins Job
On Ur AWS Console, search for Code build, and create a project. this service is paid based on the number of build time used <img width="951" height="877" alt="Screenshot 2025-10-20 121109" src="https://github.com/user-attachments/assets/406fea2f-1ff3-410a-a2d5-e8ebcddcfc41" /> 
it takes all its stages, and steps info from the build spec file earlier created.
<img width="953" height="903" alt="Screenshot 2025-10-20 121212" src="https://github.com/user-attachments/assets/34d2fb95-2ed9-4760-aac3-43958bfd15a1" />

scroll down to select the source code(Bitbucket)

<img width="942" height="903" alt="Screenshot 2025-10-20 121256" src="https://github.com/user-attachments/assets/120d7f4e-2bd7-471f-943b-3f191aedd86d" />
its shows error message gat aws is not connected to our bitbucket, lets fix that:
lets click on that 'manage account credentials' so we can link our bitbucket account
<img width="918" height="818" alt="Screenshot 2025-10-20 121548" src="https://github.com/user-attachments/assets/f7c8bbca-0b23-47f7-9241-512e733a70a4" />
on the credential type select the bitbucket app, click on 'create a new bitbucket connection' give it a name and clicked on 'connect to bitbucket'.
####Note: for AWS-Bitbucket connection to work, make sure to log in Ur bitbucket account on the same browser U loged in Ur AWS 

<img width="946" height="919" alt="Screenshot 2025-10-20 121745" src="https://github.com/user-attachments/assets/9d2fd3f8-ff23-40a3-a5af-f340a584c49b" />
it will promt for you to grant access, grant the access to connect.


<img width="937" height="904" alt="Screenshot 2025-10-20 144145" src="https://github.com/user-attachments/assets/b3479263-8bc6-4173-a265-5c265c71515b" />

Once successfully connected, you will be able to see all your bitbucket repositories, select the repo, and the branch name


