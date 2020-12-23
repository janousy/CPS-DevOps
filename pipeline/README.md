We set up the CPS Sorter on a GPU server that can be accessed through Jenkins, a continous integration tool, where a push or pull request on the github repository triggers the jenkins pipeline.
The idea is to have a jenkins server running so that the pipeline can execute always but for the sake of this project we have decided to only run the jenkins pipeline locally & leave the implementation of a jenkins node as future work.
The steps that we did where:
### Step 1
Install Jenkins and added the following plugins: 
<br />a) GitHub Pull Request Builder in order to be able to trigger pipeline builds from pull requests.
<br />b) [SSH Pipeline Steps](https://www.jenkins.io/doc/pipeline/steps/ssh-steps/) in order to execute our ssh commands on the remote server in the jenkins file.

### Step 2
In Jenkins added our SSH credentials through Manage Jenkins > Manage Credentials ![](https://github.com/janousy/CPS-DevOps/blob/main/pipeline/resources/credentials.png)
### Step 3
Created a new pipeline via "New Item > Pipeline" and in the pipeline settings we specify which github project should be tracked, the pipeline triggers (in this case push and pull requests)
and finally we defined the Pipeline Script.

### Step 4 
In the github project in "Settings > Webhooks" we add a new webhook and add our Jenkins URL as the Payload URL. Now because we are running Jenkins locally we do not have a valid
URL to set as Payload so we made use of [ngrok](https://ngrok.com/) to expose a the local development server to the Internet with minimal effort and use it's URL as payload.
![](https://github.com/janousy/CPS-DevOps/blob/main/pipeline/resources/ngroki.png)
![](https://github.com/janousy/CPS-DevOps/blob/main/pipeline/resources/githubwebhook.png)
