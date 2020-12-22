# Introduction

Besides setting up a pipeline to evaluate scenarios using the CPS-Sorter based on BeamNG and thereby classifying, we analyzed other safety critical aspects of scenarios. To do so, we examined other simulators to analyze scenarios manually. We decided for Carla - an open-source simulator for autonomous diving research - because of its active community, extensive documentation and support for Windows and Ubuntu. Carla provides a simulation server and enables multiple client connections. Moreover, developers provide a baseline autonomous driving agent.

In order to run and evaluate scenarios, we used the ScenarioRunner, provided by the same developers of Carla. Users can build their own scenarios using a defined Python Interface or the OpenScenario standard. Additionally, an initial set of scenarios is provided in their repository. The ScenarioRunner also lets users evaluate their autonomous driving agent in customizable scenarios.

We used a slightly modified version of the baseline AI agent of Carla and the pre-existing scenarios of the ScenarioRunner in order the define other safety critical aspect of scenarios. We defined a checklist with safety aspects and multiple levels. We than run our version of the AI agent in all provided scenarios and evaluated using the checklist.

Useful links:

- Carla Setup: <https://carla.readthedocs.io/en/latest/start_quickstart/>
- Scenario Runner: <https://github.com/carla-simulator/scenario_runner>
- Scenario Runner Doc: <https://carla-scenariorunner.readthedocs.io/en/latest/>

# Installation and setup

## Getting ScenarioRunner up and ready:

(This manual uses Anaconda to set up a python environment, other options can be used as well)

- Set up Carla precompiled

  - <https://carla.readthedocs.io/en/latest/start_quickstart/>

- set up an environment e.g. with Anaconda

- install required python packages:

  `pip install ~carla/PythonAPI/requirements.txt`

- Get ScenarioRunner package with **same version as installed Carla**

  - <https://github.com/carla-simulator/scenario_runner/blob/master/Docs/getting_scenariorunner.md>

### Setting up the Python Environment

- Set up a python environment that uses the same python version as Carla:

  - you can find the required version stated in the name of the .egg file:

    `%CARLA_ROOT%\PythonAPI\carla\dist\carla-0.9.10-py3.7-win-amd64.egg`

- pip install numpy pygame

- make sure correct version of networkx==2.2 is installed (see scenariorunner docs)

- `pip install -r ~/scenariorunner_root/requirements.txt`

- shapely problems: <https://towardsdatascience.com/install-shapely-on-windows-72b6581bb46c> (conda install -c conda-forge geos=3.7.1 solved the issue in our case)

- Set up environment variables:

  - <https://github.com/carla-simulator/scenario_runner/blob/master/Docs/getting_scenariorunner.md>
  - <https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#setting-environment-variables>

```
conda activate (your environment)
```

```
conda env config vars set CARLA_ROOT=PATH_TO_CARLA_ROOT
conda env config vars set SCENARIO_RUNNER_ROOT=C:\Users\janosch\Repos\scenario_runner-0.9.10
conda env config vars set PYTHONPATH=%CARLA_ROOT%\PythonAPI;%CARLA_ROOT%\PythonAPI\carla\agents;%CARLA_ROOT%\PythonAPI\carla\dist\carla-0.9.10-py3.7-win-amd64.egg
```

reactivate conda environment and check applied changes:

```
conda activate (your env)
conda env config vars list
```

# Running the ScenarioRunner

- Run Carla with low graphic mode:

  `$ ./CarlaUE4.exe -carla-server -quality-level=Low`

- (optional) check for port with admin cmd:

  `netstat -ab`

  => CarlaUE4 should be running on port 2000

- get list of scenarios available:

  `python scenario_runner.py --list`

- run scenario:

  `python scenario_runner.py --scenario FollowLeadingVehicle_1 --reloadWorld`

  if you load the automatic control:

  `python scenario_runner.py --scenario FollowLeadingVehicle_1 --reloadWorld --waitForEgo`

- activate control:

  `python manual_control.py`

  CAVEAT: both carla and scenario runner provide a script for manual control, however the one of scenario runner is recommended

- change map:

```
cd ~CARLA\PythonAPI\util\config.py
python config.py --list
python config.py --map Town01
```

# Autonomous Agent

The carla repository itself also provides automatic control of vehicles, an initial baseline for the carla challenge (<https://carlachallenge.org/>). You will find the initial file at in their [GitHub repository](https://github.com/carla-simulator/carla/tree/master/PythonAPI/examples/automatic_control.py)

This repo includes a modified version of the automatic_control.py, such that the autonomous agent can be loaded into a scenario of the ScenarioRunner. We modified this version to able to integrate it to scenarios provided by the ScenarioRunner. See the file automatic_control.py in our repository and search for 'Modded Area' without '', to find our changes.

You can find available scenarios in the file "scenarios_categorized.csv". These scenarios are initially provided by Carla ScenarioRunner, which can be found [here](https://github.com/carla-simulator/scenario_runner/tree/master/srunner/examples). A complete description of all the scenarios is available [here](https://carla-scenariorunner.readthedocs.io/en/latest/list_of_scenarios/). To be able to run the autonomous agent inside a started scenario, follow these instructions.

- select a scenario you want to run
- you may want to save (or overwrite) your file in the same location as 'carla/PythonAPI/examples/automatic_control.py' provided by the carla repository
- run the scenario:

  ```
    cd ~scenario-runner-root
    python scenario_runner.py --scenario (Scenario Name) --reloadWorld --waitForEgo
  ```

- open another console and inject the autonomous agent:

  `python automatic_control.py`

- we modified the automatic_control.py such that the spawn point, the destination and the car is no longer randomly set. After starting the script it will ask you which scenario you want to use.
- the spawn point gets automatically collected from our "scenarios_categorized.csv". Set an appropriate destination point (x,y,z) far from the spawn point since it will de-spawn as soon as it reached its destination (before the scenario_runner ends).
- we provide a default destination point: x=300, y=300, z=300, which works almost everytime for all scenarios with no intersection. 
- attention: it is possible that your defined destination point causes the AI to turn right at an intersection to reach the destination but the scenario wants it to turn left (SignalizedJunctionLeftTurn_1). In this case it is recommended to set the destination point by your own to the complete opposite direction as it often solves the problem. (x=-300, y=-300,z =-300)
- the car is set to lincoln	mkz2017 for all scenarios that got evaluated.
- the scenario_runner will independently stop if the scenario is over. The AI keeps driving until it reaches its target. You can stop further driving by hitting the ESC key.
# Scenario Classification

The following list was used to evaluate executed scenarios together with our AI agent. The full list with possible levels for each aspect is available [here](https://github.com/janousy/CPS-DevOps/blob/main/simulator/checklist.md) with . Each scenario was executed manually at least once, with adjusted spawn coordinates.

Criterium    | Description
------------ | ------------------------------------------------------------------------------------------------------------------------------------------
validity     | describes whether the provided scenario was executable. As an example, some spawn points were invalid to due being occupied by other items
city         | whether the scenario takes place inside or outside the city
lane change  | is there a lane change required, e.g. due to an object on the street or or because of overtaking a vehicle
turn         | is the vehicle required to perform a turn or does the road have curvature
safety level | dynamic or static objects included in the scenario
success      | does the AI agent successfully run through the scenario

All results obtained from the respective scenarios can be found as a CSV [here](https://github.com/janousy/CPS-DevOps/blob/main/simulator/cps_categorized.csv) in this repository.

# Future Work

**Improvements to the AI agent:**<br>
Currently, executing a scenario is rather inefficient since the spawn points for each scenario need to be adjusted in the command line. Refactoring the agent and then reading the spawn coordinates from a file indexed by scenario name would make the process a lot more efficient. 
Besides automatically integrating spawn points for scenarios, it also lacks of destination_point information for each scenario which could be added to the cps_categorized.csv. This comes along with a lot of testing.
Additionally, having a more sophisticated AI would make the evaluation of scenarios more meaningful.

**Compatibility of Scenarios and agents:**<br>
As a baseline for our AI agent, we chose the pre-built one from Carla due to time restriction. Authors of the ScenarioRunner do not recommend this procedure. Moreover, this configuration makes running scenarios error prone, for example due to spawn points being occupied. The ScenarioRunner project itself also provides an AI agent which can be extended. More detail on this can be found in the documentation of the [Carla Challenge](https://carlachallenge.org/get-started/). However, building an autonomous agent was not within the scope of our project.

**Extension of Classification Criteria**<br>
Since our agent was not very sophisticated, it was hard to obtain meaningful results during the evaluation. With a more intelligent AI and better configuration, more criteria could be used for evaluation, e.g. whether and traffic rate.

**Custom Scenarios**<br>
Again due to time restrictions, we did not build our own scenarios. Simpler scenarios would eventually make the evaulation more meaningful. The ScenarioRunner [documentation](https://carla-scenariorunner.readthedocs.io/en/latest/creating_new_scenario/) helps developers build custom scenarios.
