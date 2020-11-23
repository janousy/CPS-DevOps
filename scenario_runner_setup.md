## Running
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
	
- there's also automatic control:

	```~\CARLA_0.9.10\PythonAPI\examples\automatic_control.py"```
	
- change map: 

		```
		cd C:\Users\janosch\Repos\CARLA_0.9.10\PythonAPI\util\config.py
		python config.py --list
		python config.py --map Town01
		```


------
## Installation and setup
Getting ScenarioRunner up and ready:

- Set up Carla precompiled
- set up an environment e.g. with anaconda
- install carla python requirements.txt
- Get ScenarioRunner package with same version as Carla 
- https://github.com/carla-simulator/scenario_runner/blob/master/Docs/getting_scenariorunner.md
- Set up a python environment that uses the same python version as Carla:
	look at ~/Carla/PythonAPI/dist/carla<Version>.egg
	use for example "Anaconda" to do so
- pip install numpy pygame
- make sure correct version of networkx==2.2 is installed (see scenariorunner docs)
- cd ~/scenariorunner_root
- pip install -r requirements.txt
- shapely problems: https://towardsdatascience.com/install-shapely-on-windows-72b6581bb46c (conda install -c conda-forge geos=3.7.1 solved the issue for me)
- Set up environment variables:
	- https://github.com/carla-simulator/scenario_runner/blob/master/Docs/getting_scenariorunner.md
	- https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#setting-environment-variables

*env vars need are being reset when leaving an environement

conda activate (your env)

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

## Links
- Carla Setup: https://carla.readthedocs.io/en/latest/start_quickstart/
- Scenario Runner: https://github.com/carla-simulator/scenario_runner
- Scenario Runner Doc: https://carla-scenariorunner.readthedocs.io/en/latest/

