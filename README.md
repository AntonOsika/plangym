# Plan gym

[![Documentation Status](https://readthedocs.org/projects/plangym/badge/?version=latest)](https://plangym.readthedocs.io/en/latest/?badge=latest)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/ambv/black) 

Plan gym is an interface to use OpenAI gym for planning problems. It allows extends the standard
 interface to allow setting and recovering the environment states.
 
Furthermore, it provides functionality for stepping the environments in parallel, and it is 
compatible with passing the parameters as vectors of steps and actions.

## Getting started

### Stepping a batch of states and actions
```python
from plangym import AtariEnvironment
env = AtariEnvironment(name="MsPacman-v0",
                       clone_seeds=True, autoreset=True)
state, obs = env.reset()

states = [state.copy() for _ in range(10)]
actions = [env.action_space.sample() for _ in range(10)]

data = env.step_batch(states=states, actions=actions)
new_states, observs, rewards, ends, infos = data
```
### Using parallel steps

```python
from plangym import AtariEnvironment, ParallelEnvironment
env = ParallelEnvironment(env_class=AtariEnvironment,
                          name="MsPacman-v0",
                          clone_seeds=True, autoreset=True,
                          blocking=False)

state, obs = env.reset()

states = [state.copy() for _ in range(10)]
actions = [env.action_space.sample() for _ in range(10)]

data =  env.step_batch(states=states,
                       actions=actions)
new_states, observs, rewards, ends, infos = data
```

## Installation 

``pip3 install git+https://github.com/Guillemdb/plangym.git
``