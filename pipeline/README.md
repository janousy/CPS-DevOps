# Pipeline

To test the quality of machine lerning (ML) models, we installed the [CPS Sorter](https://github.com/billbos/CPS-SORTER) on a GPU server.
We set up a pipeline with [Jenkins](https://www.jenkins.io/) that subscribes the main branch of a github repository (in our case for testing purpose: https://github.com/solodezaldivar/SME). Whenever a commit is pushed to this repository, it is cloned into the server and Jenkins executes commands on it.
For the sake of this project, the Jenkins pipeline is hosted locally and connects to the server through an ssh connection.

The pipeline executes following commands:

- A virtual environment is created.
- The cps-sorter runs its model evaluation using test scenarios stored on the server and stores the results in a separate output folder.
- The results folder is copied to the local machine through the ssh connection.

Additionally, a third stage, that could be executed before all of the above commands, new test scenarios could be copied from the local machine to the server as well. (For this project, we commented this command and used the same scenarios for each run).

To setup your own pipeline, you can follow the installation steps [here](https://github.com/janousy/CPS-DevOps/edit/main/pipeline/installation.md).
