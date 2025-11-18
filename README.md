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
we are going to store that token on the aws parameter store.(thats our login credential)
Create New Organization by clicking the plus button <img width="1460" height="985" alt="Screenshot 2025-10-17 153328" src="https://github.com/user-attachments/assets/cfebc125-bfe4-4509-b486-944d8cad866d" /> Scroll down to select the free plan, and create the organization.

click on sonar cloud, click on Analyze new project, U'll see an option to create a project manually 
and make sure U select the recent organization U just created on the organization drop down 
select public on the project visibility.
<img width="957" height="919" alt="Screenshot 2025-10-17 153722" src="https://github.com/user-attachments/assets/470bcaa2-c64d-4978-bef1-b84900e85817" />
select the previous version, & create the project
<img width="952" height="943" alt="Screenshot 2025-10-17 161426" src="https://github.com/user-attachments/assets/db11c10f-9b42-4928-9381-455d9b2dadf5" />
Click on the recently created project Information section to copy both the project key, & the Organization key, save them on Ur notepad, those are Ur sonar Login details we will use to create parameter as defined on our builspec.yml file.
<img width="945" height="892" alt="Screenshot 2025-10-17 161856" src="https://github.com/user-attachments/assets/f0424606-5ddd-441a-b2e9-5b7752d8121c" />

***###AWS Systems Manager Parameter Store***
Based on our defined Buildspec.yml file, we are going to create a parmeter store on aws to store our Sonar Cloud Credentials. Note in terms of best practices, we are to store our credentials on AWS Secrete Manager(a Paid service), the free alternative service is the parameter store. 

<img width="955" height="787" alt="Screenshot 2025-11-13 142250" src="https://github.com/user-attachments/assets/c9ae670d-52cc-4af0-9c4e-345e07441874" />

search for system manager from Ur aws Console, scroll down the left panel and click on the parameter store as seen above, we are going to create 4 parameters for our credencials copied from the Sonar Cloud server:
   1. LOGIN parameter
   2. HOST Parameter
   3. Organization Parameter
   4. Project parameter
<img width="947" height="881" alt="Screenshot 2025-11-13 142456" src="https://github.com/user-attachments/assets/d5705195-de47-42a2-9c3a-0444a89aedb0" />
storing the organization token earlier copied from sonarcloud
scroll down and paste the organization token on the value box
<img width="949" height="892" alt="Screenshot 2025-11-13 142511" src="https://github.com/user-attachments/assets/d513edce-4079-4126-9ec5-13f7f8e6621f" />
create the parameter.
*Repeat Same step to create Project parameter store using the project token earlier copied, and HOST (https://sonarcloud.io paste that link on the value section while creating HOST paramete.) thats sonarcloud Url.

when creating LOGIN parameter, select secure string on Type section
<img width="937" height="893" alt="Screenshot 2025-11-13 143100" src="https://github.com/user-attachments/assets/24fb6d5e-24fd-47bb-8b90-9f2083e1eaf6" />
<img width="910" height="962" alt="Screenshot 2025-11-13 143113" src="https://github.com/user-attachments/assets/7abc6663-8ba2-43f8-9d80-4813f14a47a1" /> 
on the value section, paste the token earlier generated on the sonacloud account settings.
<img width="916" height="857" alt="Screenshot 2025-11-13 143138" src="https://github.com/user-attachments/assets/6f20038b-202f-44cd-a6a3-6732de01a13f" />
All 4 Parameters created and token saved.
*Note: take note of spellings and the letters case sensitivity as it most be allign with buildspec.yml file.
<img width="1919" height="297" alt="Screenshot 2025-11-17 123125" src="https://github.com/user-attachments/assets/4d9f49dc-d670-4a73-b869-8dbab6d89cdc" />

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

Once successfully connected, you will be able to see all your bitbucket repositories, select the repo, and the branch name, scroll down to complete the setup

<img width="939" height="976" alt="Screenshot 2025-10-20 164059" src="https://github.com/user-attachments/assets/21d53531-d9da-41f6-a622-449e3bb8cd35" />
select the compute resources which is ec2, select Ubuntu as the operating system, select the run time image to be 7.0 and scroll down.


<img width="961" height="957" alt="Screenshot 2025-10-20 164335" src="https://github.com/user-attachments/assets/66d728f5-b353-445c-aef1-919267774064" />

select new service role and give it a name,  "roles in aws provides permission through policies" on the build spec option, 
<img width="943" height="924" alt="Screenshot 2025-11-13 145517" src="https://github.com/user-attachments/assets/d7c5f3a4-9cf5-4a62-b058-bf098113536b" />

select 'Usee a Buildspec Option' as aws will fetch the buildspec.yml file on ur bitbucket repo root directory. if otherwize Ur buildspec file is not on the root directory, U'll have to mention the part on that buildspec space.


<img width="897" height="948" alt="Screenshot 2025-10-20 164856" src="https://github.com/user-attachments/assets/76d7be40-315e-40a5-9441-3033677c93d1" />
the last phase is to configure the cloudwatch so it will alert Us if the Project fails and why it is failing. give the cloudwatch a name, a stream name and create your code build project.


<img width="1851" height="932" alt="Screenshot 2025-10-20 165158" src="https://github.com/user-attachments/assets/90e8070b-0fac-4cff-8c4e-e867aa242492" />
Our codebuild is created and ready for Us to start build, but at this stage it will fail untill we fix the parpaeter store.
lets edit back to the build project we just created: click on edit > click on environment, there we should see the service role, we need to copy that service role.


<img width="892" height="812" alt="Screenshot 2025-10-20 165742" src="https://github.com/user-attachments/assets/4023153b-f2fa-4a4c-8283-00ea894c0cab" />
copy the service role from codebuild as shown above, and lets go to the service IAM for modifications.

Search and Click IAM on Ur aws console, go to roles, and paste what we just copy to search for our project codebuild role for modification. You Should see the role which was created by codebuild as shown bellow, click on it 
<img width="962" height="970" alt="Screenshot 2025-10-20 165932" src="https://github.com/user-attachments/assets/e0c8e328-e4a3-470d-abd6-89d78e11e0c1" />

You will see permissions with two policies such as cloudwatch logs and the code build base policy
<img width="1914" height="528" alt="Screenshot 2025-10-20 170012" src="https://github.com/user-attachments/assets/3654f53e-1a14-4502-9f82-3b872b8827b4" />

Click on policies(on the left side open panel)

<img width="960" height="588" alt="Screenshot 2025-10-20 170034" src="https://github.com/user-attachments/assets/0ba2a7c8-fdb3-42cd-9220-d10754eb9a68" />
clicked on create policies, we are to create our own custorm policy and attarched the policy to the service role

<img width="980" height="930" alt="Screenshot 2025-10-20 170152" src="https://github.com/user-attachments/assets/65ddb935-4c3f-4acd-8bce-8da3b89c723e" />
select the 'systems manager', we just want to have access to the parameter store.
on the list section, check mark 'Describe Parameters' and on the read section, check mark all these section as seen below 


<img width="1513" height="716" alt="Screenshot 2025-10-21 112006" src="https://github.com/user-attachments/assets/53afe061-b55e-4600-b966-02481040e445" />

##Take note: we selected, 1 access Level parameter on the list section, and 5 access Level parameters on the read section as seen above.
click on nex when Ure through 


<img width="879" height="978" alt="Screenshot 2025-10-21 112133" src="https://github.com/user-attachments/assets/6a041d40-d5cd-4177-8b37-897119326a63" />
Gicve the Policy a name as seen above, and create 

lets go attach the recently creted policy to our project code build role
click on roles, search the our project role using the number'85' earlier attarched to the role.
click on the role

<img width="962" height="948" alt="Screenshot 2025-10-21 112317" src="https://github.com/user-attachments/assets/17a9ff00-7054-456e-8ec4-4d7a06feceaa" />

click on attarch policies, find the recently created policy and put a check mark on it as seen below, and clicked on 'add permissoin'.

<img width="969" height="833" alt="Screenshot 2025-10-21 112348" src="https://github.com/user-attachments/assets/8cc4554c-583a-4a3f-9379-1c8a8a6ae729" />

one more policy to add it 'policy to access our codeArtifact', search for codeArtifact and select 'read only access' as seen below.

<img width="1910" height="938" alt="Screenshot 2025-10-21 112525" src="https://github.com/user-attachments/assets/505c6a30-9a88-48bc-8617-46b2c2514980" />


***###Time To Run Our Build Job###***
go to CodeBuild where our project is and click on Build, is going to take some time.
<img width="1919" height="1004" alt="Screenshot 2025-11-13 151337" src="https://github.com/user-attachments/assets/1f951a14-743d-48e4-b931-a0c4c419053f" />

Your Build should be successfull if everything was well configured
<img width="1875" height="975" alt="Screenshot 2025-11-13 162109" src="https://github.com/user-attachments/assets/e4785d5f-8b5e-40f2-a4dc-617cfccccc53" />
###If fail, study the docummentation all over again

<img width="1700" height="964" alt="Screenshot 2025-11-13 214009" src="https://github.com/user-attachments/assets/6ac4b45f-5b9a-426a-b4bd-d9dc8231e0db" />

Our prjoct passed the default quality gate on the SonarCloud Server
<img width="1903" height="1024" alt="Screenshot 2025-11-13 214100" src="https://github.com/user-attachments/assets/8ca99bbd-c91d-42ec-b795-01d2e5bd0842" />
Note: on Real Production setup, Developers must have set the Quality gate Condition on the sonarcloud

<img width="1907" height="1014" alt="Screenshot 2025-11-13 214551" src="https://github.com/user-attachments/assets/50da20b9-533d-43ef-9af1-16341ada81a4" />
thats maven central store with maven depndencies repository, as we run our build job, it downlaoded all the maven dependencies and store it on the maven-central-store

***The next step is Building the Artifact and to store it in S3***
The Next Build Job to configure is the code Artifact.
the buildspec File for this Artifact is inside the 'aws-files' located in our source repo as seen below
<img width="964" height="836" alt="Screenshot 2025-11-13 214715" src="https://github.com/user-attachments/assets/ae6bc621-8371-4262-9f1b-5c4867b4c2b8" />
when creating the Code Artifact Job, we are going to specify the path of the above buildspecfile on the Job, so codebuild can fetch and use it.
Note: we are to Update line 11 of the above builspecfile, with the link on the maven-central store: clidk on view connection instructions, copy the step 3 code as seen on the below screenshot. paste the code on line 11 of Ur buildspecfile save it and commit and push to update Ur Bitbucket
<img width="932" height="717" alt="Screenshot 2025-10-20 115231" src="https://github.com/user-attachments/assets/2ea239b0-c381-4fc4-8753-fffadc9f13ed" />

when creating the Code Artifact Job, we are going to specify the path on the Job, so codebuild can fetch and use it.

****Creating The Build Artifact Job****
<img width="948" height="976" alt="Screenshot 2025-11-13 215147" src="https://github.com/user-attachments/assets/0681c133-9f30-4652-be68-c727d74d844f" />
give the project a name, on the source, select bitbucket as usual, select Ur repository, specify the bransch name as did earlier, "Remember, we had already linked our codebuild with our bitbucket", 
scroll down to Operating System and select Ubuntu, image is 7.0
On the Role name section, we still maintain the New service role
<img width="953" height="967" alt="Screenshot 2025-11-13 215456" src="https://github.com/user-attachments/assets/de5b9845-8cc8-4748-a170-13a7114890bc" />
specify our buildspec.yml file path as seen above
regarding pushing the artifact to s3 bucket, we will configure that while creating our pipeline. 

<img width="944" height="936" alt="Screenshot 2025-11-13 215711" src="https://github.com/user-attachments/assets/4a102d5c-6c4e-4cc2-a230-f9071ad612a9" />
create a cloudwatch logs
the group name will be thesame as name as our 1st build job, edit the 1st job, copy the cloudwatch groupname and use same name here. on the stream name, is Build Artifact. Click on Create Project.
dont build the job yet, lets go and edit the role, to assign policy, meaning granting permissions to enable the buuild job have access to the codeArtifact Repository.

go to IAM, Click on role on the left panel as seen below:
<img width="943" height="643" alt="Screenshot 2025-11-13 220248" src="https://github.com/user-attachments/assets/6db4d1c2-61a7-4c46-9919-4b02f244089a" /> search for the CodeArtifact Role that was created while screating the job. click on it to open, click on attach policy just like we did on the former project.

<img width="941" height="909" alt="Screenshot 2025-11-13 220505" src="https://github.com/user-attachments/assets/2251a350-8d3a-4500-a8b4-1fd90de0cb48" />

search for codeArtifact Read only Access 
<img width="941" height="909" alt="Screenshot 2025-11-13 220505" src="https://github.com/user-attachments/assets/d9c4b402-c1d2-4561-bc51-8b0d3ffe3f11" />
after selecting it, click on add permission. the read only policy(permission) will be attached to our codebuild job role.

after adding the policy, we go back to codebuild to build our recently created project
<img width="1919" height="595" alt="Screenshot 2025-11-13 220632" src="https://github.com/user-attachments/assets/f06865ab-161a-41fb-8632-a4075b9475e8" />
the codeArtifact Build was a success
<img width="1919" height="985" alt="Screenshot 2025-11-13 221523" src="https://github.com/user-attachments/assets/f0345d9c-4c32-4514-b399-9a59f7d4cee5" />

<img width="1919" height="997" alt="Screenshot 2025-11-13 221536" src="https://github.com/user-attachments/assets/e9deacc1-12b1-44a3-ba75-96527ff62ceb" />



***###Setting Up CodePipeline For Our Build Project***
before creating pipeline, we have to setup s3, and SNS that we will later link them both to our pipeline for storing Build Artifiact, and SNS for Notification

Setting Up S3 Bucket
navigate to search on aws console, type s3 and hit on create button.
<img width="949" height="823" alt="Screenshot 2025-11-13 222122" src="https://github.com/user-attachments/assets/3b34db7a-bf4e-4866-8dd3-7c1355166364" />
Give it a name and scroll down
<img width="968" height="965" alt="Screenshot 2025-11-13 222221" src="https://github.com/user-attachments/assets/cfedeeef-8c44-430f-8c95-01237447087d" />
enamble bucket key and hit on creation button
<img width="937" height="918" alt="Screenshot 2025-11-13 223233" src="https://github.com/user-attachments/assets/1f96d3a4-c8fa-482f-8664-0925733d144a" />
after succeffully created, go in and create a folder
<img width="951" height="818" alt="Screenshot 2025-11-13 223313" src="https://github.com/user-attachments/assets/5f0c76fa-8d9b-402e-9c48-94e38749b1ad" />
give the folder a name and hit on create. (we will specify the path on our pipeline)
<img width="948" height="923" alt="Screenshot 2025-11-13 223353" src="https://github.com/user-attachments/assets/f5272ba9-aa7e-4a46-9a8e-126edf1fe537" />

Setting Up SNS For Notification
navigate to search on Ur aws console, seach sns and hit on create button to create a Topic
<img width="951" height="617" alt="Screenshot 2025-11-13 223600" src="https://github.com/user-attachments/assets/399429e9-8b48-4d41-8fa3-1063538de078" />
Give it a name and scroll down to create the Topic
<img width="959" height="963" alt="Screenshot 2025-11-13 223736" src="https://github.com/user-attachments/assets/29f3e029-a428-421c-840e-887a2350894e" />
go into the topic created to create subscription 
<img width="944" height="942" alt="Screenshot 2025-11-13 223805" src="https://github.com/user-attachments/assets/13ef4d26-2e43-4aa1-9540-4a19709fb832" />
select Email service on the protocol, insert the email addresses You wants to send notification regarding the success or failure of your pipeline 
<img width="936" height="957" alt="Screenshot 2025-11-13 223917" src="https://github.com/user-attachments/assets/afad684e-a867-494b-870e-de7c87d961f6" />
Hit on create button once done, an email notitfication will be sent to those email for confirmation once created.
<img width="1320" height="384" alt="Screenshot 2025-11-13 224518" src="https://github.com/user-attachments/assets/7186149f-c009-4db6-9ae6-eaa64874eda3" />
check your mail to Confirm the notification (check spam if U didnt seee it).
<img width="1899" height="665" alt="Screenshot 2025-11-13 224539" src="https://github.com/user-attachments/assets/793d8957-b112-4e6c-a618-22640261771d" />
thats the subscription details
<img width="644" height="401" alt="Screenshot 2025-11-13 224554" src="https://github.com/user-attachments/assets/687172d0-9d4a-408d-b26f-9439bedf92d4" />
after confirmations
<img width="962" height="900" alt="Screenshot 2025-11-13 224633" src="https://github.com/user-attachments/assets/1b15b3e8-83f1-4c96-841f-4048f5f2b11f" />
it should shows confirmed on Ur SNS.

***###Setting Up Our Pipeline***
Search for codePipeline and Hit Create Button
<img width="969" height="948" alt="Screenshot 2025-11-13 225203" src="https://github.com/user-attachments/assets/50dd5360-a8bb-455c-b389-2223557f6a90" />
<img width="957" height="654" alt="Screenshot 2025-11-14 150630" src="https://github.com/user-attachments/assets/e4f18c53-8e17-4fae-ae4d-61961d584bf5" />
select Build Custom pipeline as seen above and next
<img width="956" height="993" alt="Screenshot 2025-11-14 150720" src="https://github.com/user-attachments/assets/afd1c8b7-69b9-4fba-b48c-296b941b7274" />
specify your pipeline name, on the service role section, select new service role(role in aws relates to permisions)
<img width="933" height="952" alt="Screenshot 2025-11-13 225641" src="https://github.com/user-attachments/assets/a63a16d2-8484-40ad-9864-5f6679906f67" />
select bitbucket on the source section(meaning where is Ur source code repo)
we need to connect our Bitbucket repo with our code Pipeline(Make sure Ur bitbucket is loged in using thesame browser.)
Click on 'connect to bitbucket' as shown in the aboce screen shot.
<img width="617" height="672" alt="Screenshot 2025-11-13 230114" src="https://github.com/user-attachments/assets/45f45f1b-341f-413d-a483-d89afeb562a3" />
the above mini window appear, give a connection name(any name) and click on 'connect to bitbucket' button
<img width="597" height="618" alt="Screenshot 2025-11-13 230135" src="https://github.com/user-attachments/assets/8be68b27-8564-4efb-82eb-3892383f01ee" />
Another Mini Windows appear, click on 'install a new app' as seen above
<img width="619" height="656" alt="Screenshot 2025-11-13 230155" src="https://github.com/user-attachments/assets/48d6ad76-dc7e-4010-a7d2-f5d3febdd1a5" />
grnat the access to connect
<img width="609" height="692" alt="Screenshot 2025-11-13 230231" src="https://github.com/user-attachments/assets/cbdef2e3-2b51-4657-b1a2-8b4f897ce9d2" />
finally click on connect
<img width="945" height="965" alt="Screenshot 2025-11-13 230312" src="https://github.com/user-attachments/assets/38c669ec-c1f9-4f15-b5fd-1d19911fc89e" />
once connected, click on 'Repository name' all Ur repos on bitbucket should appear there, select this project repo
click on the 'default branch' to select our project branch, scroll down to select webhook as seen below.
<img width="955" height="962" alt="Screenshot 2025-11-14 151222" src="https://github.com/user-attachments/assets/c45fde04-5ba9-4dc7-ac39-85161680e657" />
hit on next
<img width="1781" height="626" alt="Screenshot 2025-11-15 135212" src="https://github.com/user-attachments/assets/557fa579-6fea-41f4-9242-6ce1bf062adc" />
on the Build stage above, select other build providers
click on the drop down menu to select CodeBuild
<img width="926" height="877" alt="Screenshot 2025-11-18 161837" src="https://github.com/user-attachments/assets/86a10488-3f1c-4c42-9a84-8d82ac0e4de2" />
below that 'project name' click on the search to add your project(remember we earlier build 2 projects on codeBuild as shown below, select one of the project and continue.)
<img width="1918" height="537" alt="Screenshot 2025-11-13 221913" src="https://github.com/user-attachments/assets/231e0292-f1e7-4024-9ae7-e77db232ea02" />
after selecting Ur project, skip the other sections and get to this phase as shown below, we will edit our pipeline to add the rest lster
<img width="927" height="961" alt="Screenshot 2025-11-14 152559" src="https://github.com/user-attachments/assets/6ac69541-c046-4f16-8590-83b28247640d" />
AWS CodePipeline is configured to start building automatically once created. after hitting that create button, Ur pipeline start running
<img width="959" height="935" alt="Screenshot 2025-11-14 152649" src="https://github.com/user-attachments/assets/8c660f20-be16-4ef2-a342-1ba1264f478e" />
stop the pipeline as shown above, click on stop, a small box appears as seen above, select the current execution and click on stop. it will halt the pipeline, we need to edit the pipeline so we can add other things like: the remianing codebuild job, the s3, and the sns. (i didnt add those sections before because i wanted us to learn how to edit and fix a pipeline. thats what we will be doing most of the time as a DevOps Enginner)
<img width="950" height="921" alt="Screenshot 2025-11-14 152702" src="https://github.com/user-attachments/assets/ceb8f0cf-2de0-47e5-b7a9-d1e4177375c5" />
the pipeline was halted, so we can edit to add other sections
click on edit as seen above
<img width="945" height="918" alt="Screenshot 2025-11-14 153256" src="https://github.com/user-attachments/assets/38516791-8d62-4087-9d76-8e06ccf20d29" />
click on add stage after source section as seen above
give the stage a name(trying to add the remaining codeBuild Job to this section)
<img width="948" height="887" alt="Screenshot 2025-11-14 153314" src="https://github.com/user-attachments/assets/f4fbf9ac-f2a8-4149-afe7-58eb21e6c7f2" />
click on 'Add action group' to add Ur build project
<img width="886" height="1018" alt="Screenshot 2025-11-14 153459" src="https://github.com/user-attachments/assets/7c175bbd-9a18-44fe-821e-bc6bb377b932" />
give the job a descriptive name, select aws CodeBuild on the 'action provider menu'
on 'input artifact' select sourceArtifact, on the 'project name', click to select the remaining project and click on done
scroll down to the last of the page and click on 'Add stage'
name the stage 'Deploy' (adding our s3 bucket earlier created)
once created click 'add action group' to add our s3
<img width="952" height="1015" alt="Screenshot 2025-11-14 154049" src="https://github.com/user-attachments/assets/a2347534-80fc-4eeb-b7db-8528fc09d93b" />

as seen above, give a name, select s3 on 'action provider'
search for the bucket by clicking the search field below the Bucket to select the s3 bucket earlier created as seen above
on that deployment path, write down the exact name of the folder U earlier created inside s3. the exalt name should be given here if not, Ur pipeline will fail
click on done once ure through, ####Note click on 'Done' on every stage edited, and lastly, scroll up the page to click on 'save' so that our changes can be saved.

####To add our SNS notification earier created to our pipeline, navigate to the left side of our project and click on settings as seen below
<img width="1919" height="874" alt="Screenshot 2025-11-14 154600" src="https://github.com/user-attachments/assets/0e2261aa-36f4-487d-a58f-6d31df9f5786" />
give the notification a name as seen below
<img width="950" height="963" alt="Screenshot 2025-11-14 154735" src="https://github.com/user-attachments/assets/d042385c-da80-45ce-90ff-298f2317f221" />
on the 'events that trigger notification' section, select and mark the list of trigger events you want to recieve 

<img width="936" height="961" alt="Screenshot 2025-11-14 154934" src="https://github.com/user-attachments/assets/8042ed98-c55f-4196-93f1-aff232d886cf" />
on the target section as seen above, select sns topic, and choose a target, on the search button, select the topic we earlier ccreated for the purpose of this pipeline, click on submit after that.

rerun your pipeline as seen below
<img width="1905" height="835" alt="Screenshot 2025-11-16 081042" src="https://github.com/user-attachments/assets/a5a93f36-7547-418d-a9cf-6a89679a0867" />

**##Note if your pipeline is well setup, the only reason Ur pipeline can fail is insurficient permmision**
once your codeBuild has no error, that it the build stage was a success, the pipeline has no reason to fail, except if the pipeline role doesnt have enough permission.
how do we address that?
once the pipeline fails, we study the error to be a permission issues, we simply go to IAM, click on roles at the left panel and search for ur pipeline role
###also be aware that **We cannot change the Role of a pipeline after created** we can only edit the Role to add the neccessary permissions.





