## Installation and setup

Useful links:
- Carla Setup: https://carla.readthedocs.io/en/latest/start_quickstart/
- Scenario Runner: https://github.com/carla-simulator/scenario_runner
- Scenario Runner Doc: https://carla-scenariorunner.readthedocs.io/en/latest/

### Getting ScenarioRunner up and ready:
(This manual uses Anaconda to set up a python environment, other options can be used as well)

- Set up Carla precompiled
	- https://carla.readthedocs.io/en/latest/start_quickstart/
- set up an environment e.g. with Anaconda
	- This manual uses Anaconda to set up the environment!
- install carla python requirements:
	- ~carla/PythonAPI/requirements.txt
- Get ScenarioRunner package with same version as Carla 
	- https://github.com/carla-simulator/scenario_runner/blob/master/Docs/getting_scenariorunner.md

Setting up the Python Environment
- Set up a python environment that uses the same python version as Carla:
	- you can find the version at:  ~/Carla/PythonAPI/dist/carla<Version>.egg
- pip install numpy pygame
- make sure correct version of networkx==2.2 is installed (see scenariorunner docs)
- cd ~/scenariorunner_root
- pip install -r requirements.txt
- shapely problems: https://towardsdatascience.com/install-shapely-on-windows-72b6581bb46c (conda install -c conda-forge geos=3.7.1 solved the issue for me)
- Set up environment variables:
	- https://github.com/carla-simulator/scenario_runner/blob/master/Docs/getting_scenariorunner.md
	- https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#setting-environment-variables


```
conda activate (your env)
```

```
conda env config vars set CARLA_ROOT=C:\Users\janosch\Repos\CARLA_0.9.10
conda env config vars set SCENARIO_RUNNER_ROOT=C:\Users\janosch\Repos\scenario_runner-0.9.10
conda env config vars set PYTHONPATH=%CARLA_ROOT%\PythonAPI;%CARLA_ROOT%\PythonAPI\carla\agents;%CARLA_ROOT%\PythonAPI\carla\dist\carla-0.9.10-py3.7-win-amd64.egg
```
or best without variables to prevent issues
```
conda env config vars set CARLA_ROOT=C:\Users\janosch\Repos\CARLA_0.9.10"
conda env config vars set SCENARIO_RUNNER_ROOT=C:\Users\janosch\Repos\scenario_runner-0.9.10"
conda env config vars set PYTHONPATH=C:\Users\janosch\Repos\CARLA_0.9.10\PythonAPI;C:\Users\janosch\Repos\CARLA_0.9.10\PythonAPI\carla;C:\Users\janosch\Repos\CARLA_0.9.10\PythonAPI\carla\agents;C:\Users\janosch\Repos\CARLA_0.9.10\PythonAPI\carla\dist\carla-0.9.10-py3.7-win-amd64.egg
```

reactivate conda environment and check applied changes:
```
conda activate (your env)
conda env config vars list
```

## Running the Scenario Runner
- Run Carla with low graphic mode: 

	```$ ./CarlaUE4.exe -carla-server -quality-level=Low```
- (optional) check for port with admin cmd:

	```netstat -ab```

	=> CarlaUE4 should be running on port 2000
- get list of scenarios available:

	```python scenario_runner.py --list```

- run scenario:

	```python scenario_runner.py --scenario FollowLeadingVehicle_1 --reloadWorld```
	
	if you load the automatic control:
	
	```python scenario_runner.py --scenario FollowLeadingVehicle_1 --reloadWorld --waitForEgo```

- activate control:

	```python manual_control.py```
	
	CAVEAT: both carla and scenario runner provide a script for manual control, however the one of scenario runner is recommended

- change map: 

```
cd ~CARLA\PythonAPI\util\config.py
python config.py --list
python config.py --map Town01
```

## Autonomous agents in scenarios

The carla repository itself also provides automatic control of vehicles, an initial baseline for the carla challenge (https://carlachallenge.org/) 

You will find the initial file at https://github.com/carla-simulator/carla/tree/master/PythonAPI/examples/automatic_control.py

	```cd ~\carla\PythonAPI\examples\automatic_control.py```

This repo includes a modified version of the automatic_control.py, such that the agent can be loaded into a scenario of the scenario runner.

We modified this version to able to integrate it to scenarios provided by the scenario runner. See the file automatic_control.py in this repos and search for "modded area" to find our changes.

To be able to run the autonomous agent inside a started scenario, follow these instructions.
You can find available scenarios in the file "scenarios_categorized.csv". These scenarios are initially provided by Cara Scenario Runner, which can be found here: https://github.com/carla-simulator/scenario_runner/tree/master/srunner/examples

- select a scenario you want to run
- adjust spawn location according to provided coordinates:
```
# Modded Area
            # if spawn_points[0].location != agent.vehicle.get_location():
            #    destination = spawn_points[0].location
            # else:
            #     destination = spawn_points[1].location
            destination = spawn_points[0]
            destination.location.x = 145
            destination.location.y = 200
            destination.location.z = 200
            destination = destination.location
```
- you may want to save your file in the same location as 'manual_control.py' provided by the scenario runner
- run the scenario:

	```cd ~scenario-runner-root```
	```python scenario_runner.py --scenario FollowLeadingVehicle_1 --reloadWorld --waitForEgo```

- open another console and start the automatic control:

	```python automatic_control.py```	


