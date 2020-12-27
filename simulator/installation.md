# Installation and setup

The following instructions provide a walkthrough on how to setup the ScenarioRunner together with Carla.

Requirements:

- Server side: A 4GB minimum GPU will be needed to run a highly realistic environment. A dedicated GPU is highly advised for machine learning.
- Client side: Python is necessary to access the API via command line. Also, a good internet connection and two TCP ports (2000 and 2001 by default).
- System requirements: Any 64-bits OS should run CARLA. However, since release 0.9.9, CARLA cannot run in 16.04 Linux systems with default compilers. These should be upgraded to work with CARLA.
- Other requirements. Two Python modules: Pygame to create graphics directly with Python, and Numpy for great calculus.

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

``` cd ~CARLA\PythonAPI\util\config.py python config.py --list python config.py --map Town01
