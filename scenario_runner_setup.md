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
	
- there's also automatic control, spawn_point has to be modified according to scenario list in the .py file (Ctrl + F: Modded):

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
## Cars:
0 ['vehicle', 'citroen', 'c3']

1 ['vehicle', 'chevrolet', 'impala']

2 ['vehicle', 'audi', 'a2']

3 ['vehicle', 'nissan', 'micra']

4 ['vehicle', 'carlamotors', 'carlacola']

5 ['vehicle', 'audi', 'tt']

6 ['vehicle', 'bmw', 'grandtourer']

7 ['vehicle', 'harley-davidson', 'low_rider']

8 ['vehicle', 'bmw', 'isetta']

9 ['vehicle', 'dodge_charger', 'police']

10 ['vehicle', 'jeep', 'wrangler_rubicon']

11 ['vehicle', 'mercedes-benz', 'coupe']

12 ['vehicle', 'mini', 'cooperst']

13 ['vehicle', 'nissan', 'patrol']

14 ['vehicle', 'seat', 'leon']

15 ['vehicle', 'toyota', 'prius']

16 ['vehicle', 'yamaha', 'yzf']

17 ['vehicle', 'kawasaki', 'ninja']

18 ['vehicle', 'bh', 'crossbike']

19 ['vehicle', 'tesla', 'model3']

20 ['vehicle', 'gazelle', 'omafiets']

21 ['vehicle', 'tesla', 'cybertruck']

22 ['vehicle', 'century', 'diamondback']

23 ['vehicle', 'audi', 'etron']

24 ['vehicle', 'volkswagen', 't2']

25 ['vehicle', 'lincoln', 'mkz2017']

26 ['vehicle', 'mustang']

27 ['vehicle', 'lincoln2020', 'mkz2020']

## Links
- Carla Setup: https://carla.readthedocs.io/en/latest/start_quickstart/
- Scenario Runner: https://github.com/carla-simulator/scenario_runner
- Scenario Runner Doc: https://carla-scenariorunner.readthedocs.io/en/latest/

## Scenario List
- ChangeLane_1, x="284.4" y="16.4" z="2.5" yaw="-173", no
- ChangeLane_2
- ControlLoss_1, no
- ControlLoss_2
- ControlLoss_3
- ControlLoss_4
- ControlLoss_5
- ControlLoss_6
- ControlLoss_7
- ControlLoss_8
- ControlLoss_9
- ControlLoss_10
- ControlLoss_11
- ControlLoss_12
- ControlLoss_13
- ControlLoss_14
- ControlLoss_15, no
- !! CutInFrom_left_Lane,  x="284.4" y="16.4" z="2.5" yaw="180" model="vehicle.lincoln.mkz2017", yes
- CutInFrom_right_Lane,  x="284.4" y="16.4" z="2.5" yaw="180" model="vehicle.lincoln.mkz2017", yes
- FollowLeadingVehicle_1 x="107" y="133" z="0.5" yaw="0" model="vehicle.lincoln.mkz2017"
- !! FollowLeadingVehicleWithObstacle_1  x="107" y="133.5" z="0.5" yaw="0" model="vehicle.lincoln.mkz2017"
- FollowLeadingVehicle_2
- FollowLeadingVehicleWithObstacle_2
- FollowLeadingVehicle_3
- FollowLeadingVehicleWithObstacle_3
- FollowLeadingVehicle_4
- FollowLeadingVehicleWithObstacle_4
- FollowLeadingVehicle_5
- FollowLeadingVehicleWithObstacle_5
- FollowLeadingVehicle_6
- FollowLeadingVehicleWithObstacle_6
- FollowLeadingVehicle_7
- FollowLeadingVehicleWithObstacle_7
- FollowLeadingVehicle_8
- FollowLeadingVehicleWithObstacle_8
- FollowLeadingVehicle_9
- FollowLeadingVehicleWithObstacle_9
- FollowLeadingVehicle_10
- FollowLeadingVehicleWithObstacle_10
- FollowLeadingVehicle_11
- FollowLeadingVehicleWithObstacle_11
- FreeRide_1
- FreeRide_2
- FreeRide_3
- FreeRide_4  x="269" y="-246" z="0" yaw="0" model="vehicle.tesla.model3"
- MultiEgo_1
- MultiEgo_2
- OtherLeadingVehicle_1
- OtherLeadingVehicle_2
- OtherLeadingVehicle_3
- OtherLeadingVehicle_4
- OtherLeadingVehicle_5
- OtherLeadingVehicle_6
- OtherLeadingVehicle_7
- OtherLeadingVehicle_8
- OtherLeadingVehicle_9
- OtherLeadingVehicle_10
- NoSignalJunctionCrossing
- !! StationaryObjectCrossing_1, x="7.63" y="109.91" z="1.22" yaw="359"
- DynamicObjectCrossing_1, x="7.63" y="109.91" z="1.22" yaw="359"
- StationaryObjectCrossing_2
- DynamicObjectCrossing_2
- StationaryObjectCrossing_3
- DynamicObjectCrossing_3
- StationaryObjectCrossing_4
- DynamicObjectCrossing_4
- StationaryObjectCrossing_5
- DynamicObjectCrossing_5
- StationaryObjectCrossing_6
- DynamicObjectCrossing_6
- StationaryObjectCrossing_7
- DynamicObjectCrossing_7
- StationaryObjectCrossing_8
- DynamicObjectCrossing_8
- DynamicObjectCrossing_9
- ManeuverOppositeDirection_1,  x="17" y="136" z="2" yaw="0"
- ManeuverOppositeDirection_2
- ManeuverOppositeDirection_3
- ManeuverOppositeDirection_4
- OppositeVehicleRunningRedLight_1 x="126.4" y="55.2" z="1" yaw="180"
- OppositeVehicleRunningRedLight_2
- OppositeVehicleRunningRedLight_3
- OppositeVehicleRunningRedLight_4
- OppositeVehicleRunningRedLight_5
- SignalizedJunctionLeftTurn_1  x="-133.7" y="137.4" z="0.2" yaw="0"
- SignalizedJunctionLeftTurn_2
- SignalizedJunctionLeftTurn_3
- SignalizedJunctionLeftTurn_4
- SignalizedJunctionLeftTurn_5
- SignalizedJunctionLeftTurn_6
- SignalizedJunctionRightTurn_1, x="53" y="128.1" z="1" yaw="178"
- SignalizedJunctionRightTurn_2
- SignalizedJunctionRightTurn_3
- SignalizedJunctionRightTurn_4
- SignalizedJunctionRightTurn_5
- SignalizedJunctionRightTurn_6
- SignalizedJunctionRightTurn_7
- VehicleTurningRight_1
- VehicleTurningLeft_1
- VehicleTurningRight_2
- VehicleTurningLeft_2
- VehicleTurningRight_3
- VehicleTurningLeft_3
- VehicleTurningRight_4
- VehicleTurningLeft_4
- VehicleTurningRight_5
- VehicleTurningLeft_5
- VehicleTurningRight_6
- VehicleTurningLeft_6
- VehicleTurningRight_7
- VehicleTurningLeft_7
- VehicleTurningRight_8
- VehicleTurningLeft_8
- CARLA:PedestrianCrossing (OpenSCENARIO)
- CARLA:ChangingWeatherExample (OpenSCENARIO)
- CARLA:CyclistCrossing (OpenSCENARIO)
- CARLA:FollowLeadingVehicle (OpenSCENARIO)
- CARLA:LaneChangeSimple (OpenSCENARIO)
- CARLA:ControllerExample (OpenSCENARIO)
- CARLA:PedestrianCrossing (OpenSCENARIO)
