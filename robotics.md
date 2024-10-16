# self learning course notes on robotics

## basics

- bayes rule
  - relates conditional of type p(x|y) to its inverse p(y|x)
  - p(x|y) = (p(y|x) * p(x)) / p(y)
  - practical application/interpretation
    - y is data, sensor measurement
    - x is a quantity that we want to infer
    - p(x) 
      - prior probability distribution
      - knowledge we have regarding x prior to incorporating the data y
    - p(x|y)
      - posterior probability distribution
    - in other words: inferring quantity x from sensor data y

- automated guided vehicle (agv)

- odometric drift: discrepancy between calculated and actual state


## fleet software

- fleet monitoring software
  - provides current status of the fleet
  - allows to remotely control individual robots
  - companies: freedom robotics, braincorp

- fleet management software
  - products: mir fleet, omron fleet, otto fleet manager, fetchcore software, in orbit


## standards

- sdf (simulation description format)
  - describes objects and environments for robot simulators, visualization, and control

- urdf (unified robotics description format)
  - is an XML specification
  - used in academia and industry to model multibody systems
    - e.g. robotic manipulator arms for manufacturing assembly lines and animatronic robots for amusement parks
  - supported by ros, dart

- vda 5050
- massrobotics interop 
- open-rmf


## quadruped robots

- mit cheetah 3 mechanics paper
  - low cost modular actuator for dynamic robots https://dspace.mit.edu/handle/1721.1/118671
  - uses brushless motors with planetary gearset reducers
    - small, cheapest one 38 USD https://www.aliexpress.com/item/10000004058286.html
    - best one 450 USD https://www.aliexpress.com/item/10000018030781.html
  - controller should support torque control of the motor
    - otherwise you'll have to simulate it on a software level or something like that


## foss toy robots

- opencat framework https://github.com/PetoiCamp/OpenCat
  - robodog bittle https://www.indiegogo.com/projects/bittle-a-palm-sized-robot-dog-for-stem-and-fun
  - robocat nybble https://www.indiegogo.com/projects/nybble-world-s-cutest-open-source-robotic-cat
  - assembling https://www.youtube.com/playlist?list=PLHMFXft_rV6MJ-BhDN-O5I_u4YeAie30n


## commercial toy robots

- digital dream labs (ex anki)
  - idea behind anki robot was pretty cool
  - however i've got a deficient/autistic one
    - which suppose to be symbolic i guess

- hadabot https://www.hadabot.com/purchase.html
  - turtle robot
  - ros2 compatible


## top robotic companies [10]

- industrial
  - kuka
    - german company, owned by the chinese company midea group since 2016

  - fanuc (Fuji Automatic NUmerical Control)
    - japanese group of companies
    - largest maker of industrial robots in the world
    - automation products and services such as robotics and computer numerical control wireless systems

  - abb

  - yaskawa electric

  - epson robotics
    - japanese company
    - design and construction of robotics for factory automation

  - rocketwell automation

- retail
  - zebra technologies

- zoomorphic/humanoid
  - hyundai boston dynamics


## other robotic companies

- agility robotics
  - recently released a biped robot "digit"

- misorobotics
  - automated cooking
  - using antropomorphic hand and off-the-shelve kitchen appliances

- dronedeploy
  - their product 'rocos' was used by nasa to drive some robots on international space station (iss)


## related mechanics

- bowden cable (/ˈboʊdən/ BOH-dən)
  - is a type of flexible cable used to transmit mechanical force or energy by the movement 
    of an inner cable relative to a hollow outer cable housing

- stepper motor
  - brushless DC electric motor that divides a full rotation into a number of equal steps
  - the motor's position can be commanded to move and hold at one of these steps 
    - without any position sensor for feedback (an open-loop controller)
      as long as the motor is correctly sized to the application in respect to torque and speed

- servo motor
  - has a feedback circuit with potentiometer


## solvers

- discrete vs continuous solvers [8]
  - simulators are able to produce continuosly evolving states e.g. line/spline trajectory, which can be infinitely divided
    - such continuous simulation data can provide more information to the solver in order for it to come up with more accurate solution, comparing to discrete simulation
    - in contrast, realtime mode is always discrete

- implicit vs explicit integration: tbd
  - implicit methods need some information about the next state of a system in order to solve for current one


## foss libraries

- https://github.com/AtsushiSakai/PythonRobotics
- https://github.com/ros2
- https://github.com/hybridgroup/gobot
- https://github.com/rwaldron/johnny-five
- https://dartsim.github.io/index.html


## frameworks

### open-rmf

- description
  - foss
  - modular software system that enables robotic system interoperability
  - coordinates multiple fleets of indoor and outdoor robots with typical robotic use cases
  - integrates them with elevators/lifts, doors and other infrastructure

- features
  - schedule
  - traffic negotiation
  - task dispatch auctions


### ros2 (robotic operational system)

- not a real os but just an sdk for robotics

- distributions
  - rolling ridley: rolling release with latest features
  - humble hawksbill (latest, as of nov 2022)
    - released on may 2022

- uses data distribution service (DDS) standard that provides interface to pub-sub middleware implementations 
- uses colcon tool to manage environments, build and test code in ros

- key concepts
  - graph
    - network of ros elements processing data together
    - processes are represented as nodes in a graph structure
  - nodes
    - communicate with each other using topics and services
    - have parameters, configuration value of a node
    - can have a managed lifecycle: a configurable state machine in charge of initialization and shutdown of the node
  - topics
    - used for publish/subscribe communication
  - services
    - used for request/response communication
  - actions
    - provide functionality for setting a goal and receiving a feedback
    - implemented using of services and topics
  - message types
    - data structure defining a message format used when interacting with a services, topics, actions
  - bags
    - tool for recording, and replaying data
    - use sqlite behind the scenes to store data
    - commands: record, play, and info
  - parameter server
    - shared database

  - packages: tbd
  - workspaces: tbd

- ros2 cli commands
  - launch
    - typically configures and runs multiple nodes at the same time
    - serves as an entry point, aka main function but potentially affecting all nodes
    - can do other arbitrary things, as it is just mapped to a python script

- ros2 tools
  - colcon: builds code in multiple packages in dependency order
  - traffic_editor
    - annotates building floor plans with fleet-specific traffic information in a vendor neutral manner
    - allows auto-generation of 3d worlds for simulations

- simulators supported: gazebo, v-rep, morse, webots

- visualizers
  - rviz
    - it is a tool for visualizing data from a variety of sources, including simulations. 
    - is not a simulator in itself
    - can display 3D models of robots and their environments, as well as sensor data such as lidar, camera, and IMU readings

- vscode + devcontainer for ros2
  - https://www.allisonthackston.com/articles/vscode-docker-ros2.html

- bridges
  - ROS1_bridge
    - allows to interface ros1 robot with ros programs
    - republishes ros1 messages in ROS2 format


## simulators

- gazebo
  - is a high-fidelity physics simulator that is designed specifically for robotics applications
  - allows users to create realistic simulations of robots and their environments
  - integrates with ROS through a set of plugins
  - most popular simulator according to a survey [9]

- coppeliasim (formerly v-rep)
  - is a multi-purpose robotics simulation software that can be used to simulate robots, sensors, and environments. 
  - supports a wide range of robot platforms and can be used with ROS through a set of libraries and plugins

- morse
  - morse is a robotics simulation software that is designed to be simple and lightweight
  - it allows users to create simulations of robots and their environments using a set of simple blocks, and it integrates with ROS through a set of libraries and scripts

- webots
  - professional robotics simulation software that is used by a number of research labs and companies around the world
  - allows users to create realistic simulations of robots and their environments, and it integrates with ROS through a set of plugins and libraries


## physics engines

- foss
  - bullet https://github.com/bulletphysics/bullet3
    - used by openai gym https://github.com/openai/gym
  - ode https://www.ode.org/
  - physx https://github.com/NVIDIAGameWorks/PhysX
    - backed by nvidia
  - chrono https://github.com/projectchrono/chrono

- commercial
  - havok
  - mujoco https://mujoco.org/
  - newton dynamics http://newtondynamics.com/forum/newton.php

- benchmarks
  - https://leggedrobotics.github.io/SimBenchmark/
  - https://arxiv.org/pdf/1402.7050.pdf
    - 119 participants survey


## approaches to modelling

- behavior-based techniques 
  - do not rely on a specific model of the robot or its environment, but rather on a set of simple behaviors that can be triggered by specific stimuli
  - generally more robust to changes in the environment or the robot's internal state, as they do not rely on a specific model of the system
  - generally less flexible, as they are based on a fixed set of behaviors that are triggered by specific stimuli

- model-based techniques 
  - use a mathematical model of the robot and its environment to predict the effects of actions and to optimize control inputs
  - can handle more complex tasks and environments, as they can reason about the effects of actions over longer horizons and handle more variables
  - can be more sensitive to changes in the system, as they rely on accurate models of the system's behavior
  - can be more flexible, as they can be used to optimize control inputs to achieve a specific goal

- hybrid control architectures (hca)
  - model-based control
  - behavior-based control
  - learning
    - hca may include learning algorithms that allow the robot to adapt to new tasks and environments by adjusting its internal models or behaviors based on experience
  - decision making
    - hca often include decision making algorithms that allow the robot to select the most appropriate control approach or behavior based on the current situation


## data structures/algorithms typically used

- tbd: a-star and stuff like that

- scene graph

- octree [6]
  - tree data structure in which each internal node has exactly eight children
  - often used to partition a three-dimensional space by recursively subdividing it into eight octants
  - python bindings [7] 

- final state machine (fsm)

- behavior tree
  - nodes represent tasks
  - node types
    - action task
      - composite action task
        - fallback (tries among several alternatives)
        - sequence (list of tasks to be executed)
    - condition
      - never in a 'running' state
      - don't change the world
  - node states: running, success, failure
  - execution
    - tree is 'ticked' repeatedly
      - meaning system calls tree update method repeatedly
      - tree updates its state during tick
      - this ensures fine-grained state change while taking controlled amount of system resources
    - uses approach somewhat similar to dfs for traversing nodes
    - if node that we're visiting is in
      - 'running' state - we just stop traversal till the next tick
      - 'failed' state - execution continues to a next child of a composite node
  - advantages
    - few dependencies between components
    - modularity
    - clear graphical representation (as a tree)

- particle filter
  - represent the state of the system as a set of discrete particles, each of which represents a possible state of the system
  - update the estimate of the system state by sampling from the particles based on the likelihood of the current measurement
  - can be computationally intensive, as they require sampling and weighting a large number of particles at each time step
  - is a non-parametric filter

- gaussian filter
  - represent the state of the system as a probability distribution, typically using a Gaussian distribution
  - update the estimate of the system state by incorporating the current measurement into the probability distribution using Bayes' rule
  - generally more computationally efficient, as they only require updating a single probability distribution

- internal models approach 
  - provides a framework for understanding how robots can learn and adapt to new tasks and environments by building and adapting internal models of the relationships between actions and sensory outcomes

- balancing biped
  - zero moment point (ZMP) control 
    - is a technique that is used to balance a bipedal robot by ensuring that the robot's center of mass stays within its support polygon, which is the area that is supported by the robot's feet
    - ZMP control involves continuously adjusting the robot's posture and foot positions to maintain the center of mass within the support polygon

  - model predictive control (MPC) 
    - technique that involves using a mathematical model of the robot and its environment to predict the future state of the system and optimize the robot's control inputs to achieve a desired goal. MPC can be used to balance a bipedal robot by predicting the robot's future movements and adjusting its control inputs to maintain stability


## useful commands

- robotic operation system (ROS) related commands
  - to run "roscore" process from the "ros:latest" docker image 
    > docker run -itd --rm --name ros01 ros:latest roscore

  - attach to already running ROS container via interactive shell:
    > docker exec -ti rosmaster /opt/ros/melodic/env.sh bash

  - to list topics inside ROS container
    > rostopic list


## interesting things

- ros is often used with realtime os like rocos
  - low-level stuff is done in realtime os
    - joints solver
    - trajectory following code
  - higher-level stuff is done in ros
    - motion planning

- in space you need to plan for radiation
  - ecc memory modules provide base self-correcting algorithms
  - 3 machines are used to cross-verify commands
    - in case of detected error motion-stop command gets issued


## links

- sun and planet gears https://en.wikipedia.org/wiki/Sun_and_planet_gear
- reddit robotics https://www.reddit.com/r/robotics
- ros2 with k8 https://ubuntu.com/blog/exploring-ros-2-with-kubernetes
- ros 2 and AI on the NVIDIA Jetson Platform https://developer.nvidia.com/blog/implementing-robotics-applications-with-ros-2-and-ai-on-jetson-platform-2/
- ros multirobot book https://osrf.github.io/ros2multirobotbook/intro.html


## references

[5]: https://octomap.github.io
[6]: https://en.wikipedia.org/wiki/Octree
[7]: https://github.com/wkentaro/octomap-python
[8]: https://robotics.stackexchange.com/questions/2148/continuous-or-discrete
[9]: https://arxiv.org/pdf/1402.7050.pdf
[10]: https://www.onlinerobotics.com/news-blog/comparing-top-industrial-robotics-brands