# P10: Model Predictive Control

The project includes the following files

* CMakeLists.txt
* src folder
* notes.txt (this file)
* MPC_video02.mp4

## Description

The project was addressed the following way:

* Fill in code from quizzes to the project.
* Review the [QA session](https://youtu.be/bOQuhpz3YfU) for missing points and tips.
* Review the [Forum](https://discussions.udacity.com/c/nd013-controllers/project-model-predictive-control) messages and Slack #s-t2-p-mpc channel.
* Get basic MPC working and continue tweaking parameters.

## Considerations

I got some installation problems solved using [this](https://discussions.udacity.com/t/error-installing-ipopt/246939/) thread.

The QA session was useful to get started and get a sample working. There are subtle changes between the quizzes and QA session so it required carefully comparing both to understand the differences and why the simulation was completely wrong.

I followed these steps:

* Convert global waypoints into local frame as suggested easing math.
* Fit the waypoints with a 3rd order polynomial (f0 and psides0 variables).
* Build the constrains using parameter tuning from [this](https://discussions.udacity.com/t/mpc-cost-paramter-tuning-question/354670) thread.
* Timestep length and Elapsed duration using values of dt=0.1 and N=10, other intervals tested dt={0.1, 0.15, 0.2} and N={10, 15, 20}. 20 proved to be a high number.

For the initial submission I did not implement latency improvements as suggested [here](https://discussions.udacity.com/t/how-to-incorporate-latency-into-the-model/257391/). I just assumed that the speed will not change during the 100ms time interval because it is small enough to be constant. The car could drive up to 55mhs, but as I increased the speed it was not a good assumption.

Then, I reviewed the link and applied equations to project values accordingly and update the state vector. Now the car could drive up to 75mhs.


## Troubleshooting

These threads were useful

* [wrong calculus](https://discussions.udacity.com/t/mpc-solver-returning-nonsense-path/275606/3)
* I needed to take care of variables initialization properly in the MPC Solve method.
* All the visualization added to the simulation was extremely useful as cout statements are difficult to match to the running simulation and too much information is displayed.
* It would be nice to be more explicit on the code and detail subtleties which impacts the code and are hard to detect. Examples I found:
  * Unity conventions and how it impacts the code.
  * Measure units and related conversions such as mhs to m/s. 

## Test

Follow these steps for validation:

1. Compile the project as detailed `cmake .. && make` under the build directory.
2. Run `./mpc`
3. Run the simulator; select the correct track and start.
