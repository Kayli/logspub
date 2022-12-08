# self learning course notes on robotics


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


## top robotic companies

- kuka
  - german company, owned by the Chinese company Midea Group since 2016
- hyundai
  - because aquired boston dynamics
  - boston dynamics robots look impressive


## interesting robotic companies

- agility robotics
  - recently released a biped robot "digit"

- misorobotics
  - automated cooking? antropomorphic hand is there ... not sure why

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


## solvers

- discrete vs continuous solvers [^8]
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


## ros2 (robotic operational system)

- not a real os but just an sdk for robotics

- distributions
  - rolling ridley: rolling release with latest features
  - humble hawksbill (latest, as of nov 2022)
    - released on may 2022

- uses data distribution service (DDS) standard that provides interface to pub-sub middleware implementations 
- uses colcon tool to manage environments, build and test code in ros

- ros concepts
  - nodes
    - parameters
  - topics
  - services
    - used for sync operations
  - actions
    - used for async operations
  - message type
    - type of the message passed to a service
  - parameter server
    - communal database

- processes are represented as nodes in a graph structure, connected by edges called topics
 
- system does not fully utilize encapsulation principles in order to make system more usable
  - focuses attention of users on wrong things
	- most likely consequences of
	  - leaky abstractions
	  - poor design decisions
	  - backward compatibility constraints
  - cli commands are far from elegant
      - type inference for message types is missing
      - you should be able to omit type names in most cases
    - "send_goal" verb name is questionable: "call" would make much more sense
  - doesn't feel like elegantly designed robotics framework/solution
    - but more like a bunch of students hackery around message bus

- vscode + devcontainer for ros2
  - https://www.allisonthackston.com/articles/vscode-docker-ros2.html

- simulators
  - gazeebo
  - rviz


## data structures/algorithms typically used

- tbd: a-star and stuff like that

- octree [^6]
  - tree data structure in which each internal node has exactly eight children
  - often used to partition a three-dimensional space by recursively subdividing it into eight octants
  - python bindings [^7] 

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
[^5]: https://octomap.github.io
[^6]: https://en.wikipedia.org/wiki/Octree
[^7]: https://github.com/wkentaro/octomap-python
[^8]: https://robotics.stackexchange.com/questions/2148/continuous-or-discrete