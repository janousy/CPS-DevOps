# Installation
## Pre-Requesites
- Python v3.6
- Pip
- Supported OS: Linux, Windows
<br>
To setup a Jenkins pipeline locally, you can follow these instructions:

## Step 1

Install Jenkins and add the following plugins:<br>
a) [GitHub Pull Request Builder](https://plugins.jenkins.io/ghprb/) in order to be able to trigger pipeline builds from pull requests.<br>
b) [SSH Pipeline Steps](https://www.jenkins.io/doc/pipeline/steps/ssh-steps/) in order to execute our ssh commands on the remote server in the jenkins file.

## Step 2

Add your SSH credentials in Jenkins via `Manage Jenkins` -> `Manage Credentials` to allow us to access the GPU server in an automated manner through the JenkinsFile.

![](https://github.com/janousy/CPS-DevOps/blob/main/pipeline/resources/credentials.png)

## Step 3

Create a new pipeline via `New Item` -> `Pipeline`. In the pipeline settings, you can specify which github project should be tracked, what github processes trigger the pipeline (in this case any commit and pull request) and finally you can define the `JenkinsFile` that is stored in the repository.

![](https://github.com/janousy/CPS-DevOps/blob/main/pipeline/resources/jenkinsfile.PNG)

## Step 4

In the github project under `Settings` -> `Webhooks`, you can add a new webhook and add your Jenkins URL as the payload URL.<br>

![](https://github.com/janousy/CPS-DevOps/blob/main/pipeline/resources/webhook.png)<br>

Since we are running Jenkins locally, we do not need to set valid URL as Payload so you can make use of [ngrok](https://ngrok.com/) to expose a local development server to the Internet with minimal effort and use its URL as payload.

![](https://github.com/janousy/CPS-DevOps/blob/main/pipeline/resources/ngroki.png)
