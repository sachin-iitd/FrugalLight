# FrugalLight

FrugalLight is a reinforcement learning agent for AI based separate and independent (without network communication) 
traffic signal control. It intends to match state-of-the-art-performance using low computational resources.

The underlying code for this project has been imported from an open source project Presslight at github.

Start an experiment by:

``python code/runexp.py --transform=?``

where ? can be any prefix from Lane,Approach,Group,Relative.

## Datasets

  FrugalLight uses real data for the evaluations. Traffic file and road networks of New York City and New Delhi can be found in ``data``, 
  it contains two networks of NYC at different scales (16_1 folder contains 16 intersections and 16_3 folder contains 48 intersections), and 1_1 folder contains New Delhi data for a 3-approach single intersection.
  The 1-6 hours Delhi datasets (in cityflow simulator format) are generated from the real traffic density data available at https://delhi-trafficdensity-dataset.github.io using the script available at 
  ``utils/density2cityflow.py``

## Modules

* ``runexp.py``

  Run the pipeline under different traffic flows with various arguments/parameters. Specific traffic flow files as well as basic configuration can be assigned in this file. For details about config, please turn to ``config.py``.

  For most cases, you might only modify traffic files and config parameters in ``runexp.py`` via commandline parameters.

* ``dqn.py``

  A DQN based agent build atop ``agent.py``

* ``config.py``

  The default configuration of this project. Note that most of the useful parameters can be updated in ``runexp.py`` via command line arguments.

* ``pipeline.py``

  The whole pipeline is implemented in this module:

  Start a simulator environment, run a simulation for certain time (one round), construct samples from raw log data, update the model etc.

* ``generator.py``

  A generator to load a model, start a simulator environment, conduct a simulation and log the results.

* ``anon_env.py``

  Define a simulator environment to interact with the simulator and obtain needed data.

* ``construct_sample.py``

  Construct training samples from data received from simulator. Select desired state features in the config and compute the corresponding reward.

* ``updater.py``

  Define a class of updater for model updating.
  
## Simulator

  The project uses an open source simulator CityFlow to get the impact of FrugalLight's actions in the environment. The default library is built for Python 3.6, and a Python 3.7 variant is also provided. If the given libraries don't work for you, please build the Cityflow simulator from source code available at https://github.com/cityflow-project/CityFlow.

