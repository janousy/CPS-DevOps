# CPS DevOps

## Meeting with Bill on 5.11.20

- BeamNG is only required to provide an oracle, e.g. when generating and evaluating scenarios on the fly

    ```cps_sorter real-time-eval```

- BeamNG is not required if previously evaluated scenarios are provided

    ```cps_sorter run-model-eval -i /path/to/test/scenarios```

eval results:

![results](results.png)

- We need to adjust the model training to get classification of unsafe/safe (since not provided in results)
    
    ``` CPS-Sorter/src/cps-sorter/services/cli.py ```

- required: weka_helper.py
- wekahelper - make_bulk_predictions
- wekahelper.build_modules
- use training file "?0.4-06-split-datasetname.csv?" for training file

## Meeting with Sebastiano on 5.11.20
Split Groups:
- Ramon, Michael: CPS and Jenkings
- Alain, Gokhila, Janosch: Try Simulator with Drones (AirSim)

## Next Steps
- current no SSH connection to server
- install CPS on Server
- refactor ML pipeline
- setup Jenkins pipeline

## Meeting 12.11.2020
Simulators:
- asfault only generating test cases for BeamNG
- Carla
    - only builds for Windows/Linux, MacOs build not recommended (https://carla.readthedocs.io/en/latest/)
    - Could use OpenDrive for generating road meshes (RoadRunner required)
    - Asfault only generates env's for cars!
    - (But how to let an AI drive through this mesh?)
