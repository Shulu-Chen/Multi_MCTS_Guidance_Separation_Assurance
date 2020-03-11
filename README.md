# Multi_MCTS_Guidance_Separation_Assurance

A Python implementation of the algorithm proposed in paper "Scalable Multi-Agent Computational Guidance with Separation Assurance for Autonomous Urban Air Mobility Operations" by [Xuxi Yang](https://xuxiyang1993.github.io/) and [Peng Wei](https://web.seas.gwu.edu/pwei/).

A short video demo of this algorithm: https://www.youtube.com/watch?v=2cbRUig4G_I&t=

## Requirements

* python 3.6
* numpy
* gym
* collections
* shapely


## Optional arguments

`--save_path` the path where you want to save the output

`--seed` seed of the experiment

`--render` if render the env while running exp

`--debug` set to True if you want to debug the algorithm (the code will stop running and render the current state)

## Running the algorithm

Three case studies can be run in thie repository.

For case study 1 in the paper, run

`python Agent_vertiHexSecGatePlus.py`

For case study 2, run

`python Agent_vertiHexSecGatePlusTwoStage.py`

For case study 3, run

`python Agent_vertiport.py`


## MCTS algorithm
The code MCTS algorithm is under the directory `MCTS/`

`common.py` defines the general MCTS node class and state class

`nodes*.py` defines the MCTS node class and state class specifically for Multi Agent Aircraft Guidance proble, e.g., given current aircraft state and current action, how to decide the next aircraft state

`search_multi.py` describes the search process of MCTS algorithm

## Simulator
The simulator code is under the directory of `simulators/`. The following described the main function in simulators.

`config*.py` defines the configurable parameters of the simulator. For example, airspace width/length, number of aircraft, scale (1 pixel = how many meters), conflict/NMAC distance, cruise/max speed of aircraft, heading angle change rate of aircraft, number simulations and search depth of MCTS algorithm, vertiport location, ...

* `__init__()` initilize the simulator by generating vertiports, sectors, loading configuration parameters, and generating aircraft.

* `reset()` will reset the number of conflicts/NMACs to 0 and reset the aircraft dictionary. Note here all the aircraft objects are stored in the `AircraftDict` class, where you can add/remove aircraft from it, and get aircraft object by id.

* `_get_ob()` will return the current state, which is n by 8 matrix, where n is the number of aircraft. Each aircraft has (x, y, vx, vy, speed, heading, gx, gy) state information.

* `_get_normalized_ob()` will normalized the state to be in range [0, 1], which will be useful if we want to feed state into a neural network.

* `step()` will return next state, reward, terminal, info given current state and current action. Each aircraft will fly according the given action. We have a clock at each vertiport to decide whether to generate new flight request/aircraft.

* `_terminal_reward()` will return the reward function for current state. This function will check if there is any conflict/NMAC between any two aircraft and update conflict/NMAC number. It will also remove aircraft that reaches goal position and aircraft pair that has NMAC.

* `render()` will visualize all of the current aircraft and vertiport.

## Citing this work
If you find this codebase useful for your research work, we encourage you to cite the software using the following BibTex citation:

```
@article{yang2020scalable,
  title={Scalable Multi-Agent Computational Guidance with Separation Assurance for Autonomous Urban Air Mobility Operations},
  author={Yang, Xuxi and Wei, Peng},
  journal={Journal of Guidance, Control, and Dynamics},
  year={2020},
  publisher={American Institute of Aeronautics and Astronautics}
}
```


If you have any questions or comments, don't hesitate to send me an email! I am looking for ways to make this code even more computationally efficient.

Email: xuxiyang@iastate.edu
