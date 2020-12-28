# Pipeline
## Introduction
To test the quality of machine lerning (ML) models, we installed the [CPS Sorter](https://github.com/billbos/CPS-SORTER) on a GPU server.
We set up a pipeline with [Jenkins](https://www.jenkins.io/) that subscribes the main branch of this github repository. Whenever a commit is pushed to this repository, it is cloned into the server and Jenkins executes commands on it.
For the sake of this project, the Jenkins pipeline is hosted locally and connects to the server through an ssh connection.

## Methodology
We decided to host the Jenkins pipeline locally because we encountered workspace related issues when trying to run the cps sorter and the Jenkins pipeline on the same server.
As Jenkins then only works in an segregated workspace we couldn't access the cps_sorter command on the server. <br>
A detailed view of how we have structured the pipeline job can be seen below.

![](https://github.com/janousy/CPS-DevOps/blob/main/pipeline/resources/JenkinsArchitecture.png)

The pipeline executes following commands:

- A virtual environment is created.
- The cps-sorter runs its model evaluation using test scenarios stored on the server and stores the results in a separate output folder. The results include the recall and precision of prediciton of safe and unsafe scenarios and the training and test accuracy of each ML model. Also it returns a list of all scenarios with a label of "safe" or "unsafe".
- The results folder is copied to the local machine through the ssh connection.


Additionally, a third stage, that could be executed before all of the above commands, new test scenarios could be copied from the local machine to the server as well. (For this project, we commented this command and used the same scenarios for each run).

> To setup your own pipeline, you can follow the installation steps [here](https://github.com/janousy/CPS-DevOps/blob/main/pipeline/installation.md).

## Results
- The results that the developer will get are in the format shown below.
 ![](https://github.com/janousy/CPS-DevOps/blob/main/pipeline/resources/modelEval.PNG)


