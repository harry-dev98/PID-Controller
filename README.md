# Udacity Self-Driving Car Enginer Nanodegree -  _PID Control Project_
Self-Driving Car Engineer Nanodegree Program

---
This project aims to build a simple PID controller and tune the associated hyper-parameters to control the steering input for a self driving vehicle within the Udacity simulation environment.

---
## Tuning the PID loop

* The proportional term P produces an output value that is proportional to the current cross track error value. The effect of this on the steering control is to then steer by a proportional but opposite direction to the cars distance from the centre of the lane. If the proportional gain constant Kp was set too high this term resulted in unstable behaviour, and oscillating steering around the lane centre line was observed, ultimately throwing the vehicle off the road. With the gain constant Kp too low the controller was unable to adequately steer the vehicle around corners. It is therefore apparent that the proportional term should contribution to the majority of the output change.

* The derivative term D accounts for the gradient of the cross track error over time and the effect of this on the final steering control is scaled by the derivative gain constant Kd. This derivative term has a predictive effect on the system behaviour and reduces the impact of instabilities in the system. In practice this term can be seen to reduce tendency of the proportional term to overshoot the centre line. When Kd is correctly tuned with respect to the proportional gain constant Kp this term is found to help the vehicles steering and approach the centre line correctly.

* The integral term I is proportional to both the magnitude and duration of the cross track error. As it is computed as the sum of the cross track error over time, this then gives the accumulated offset that should have been corrected at previous timesteps. The error accumulation is then multiplied by the integral gain term Ki and added to the steering control. This term is can be used to correct for systematic bias in control systems, eg steering drift for the autonomous vehicle.

### Parameter tuning

The parameters Kp, Ki and Kd were tuned manually by incrementally observing the vehicle behaviour over many test loops within the simulation environment. With Ki and Kd set to zero, Kp was incremented until until the driving behaviour was seen to oscillate, the value of Kp was then set to be around 75% percent of this value. 

Next a small amount of Ki was added in an attempt to remove any system bias that may be present. As this was a simulation environment, is it unlikely any large system bias would be present, however this term was found to give a small performance improvement for steering in tight corner, possibility due to communication delay between the simulation and controller.

Finally the Kd was increased to reduce the oscillations and system instabilities, this increase was stopped when the vehicle was becoming detrimentally responsive.

The final parameter selected for the model were Kp = 0.09 Ki = 0.0001 Kd = 1.4







---
## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1(mac, linux), 3.81(Windows)
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets 
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

There's an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`. 

Tips for setting up your environment can be found [here](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/0949fca6-b379-42af-a919-ee50aa304e6a/lessons/f758c44c-5e40-4e01-93b5-1a82aa4e044f/concepts/23d376c7-0195-4276-bdf0-e02f1f3c665d)

## Editor Settings

We've purposefully kept editor configuration files out of this repo in order to
keep it as simple and environment agnostic as possible. However, we recommend
using the following settings:

* indent using spaces
* set tab width to 2 spaces (keeps the matrices in source code aligned)

## Code Style

Please (do your best to) stick to [Google's C++ style guide](https://google.github.io/styleguide/cppguide.html).

## Project Instructions and Rubric

Note: regardless of the changes you make, your project must be buildable using
cmake and make!

More information is only accessible by people who are already enrolled in Term 2
of CarND. If you are enrolled, see [the project page](https://classroom.udacity.com/nanodegrees/nd013/parts/40f38239-66b6-46ec-ae68-03afd8a601c8/modules/f1820894-8322-4bb3-81aa-b26b3c6dcbaf/lessons/e8235395-22dd-4b87-88e0-d108c5e5bbf4/concepts/6a4d8d42-6a04-4aa6-b284-1697c0fd6562)
for instructions and the project rubric.

## Hints!

* You don't have to follow this directory structure, but if you do, your work
  will span all of the .cpp files here. Keep an eye out for TODOs.

## Call for IDE Profiles Pull Requests

Help your fellow students!

We decided to create Makefiles with cmake to keep this project as platform
agnostic as possible. Similarly, we omitted IDE profiles in order to we ensure
that students don't feel pressured to use one IDE or another.

However! I'd love to help people get up and running with their IDEs of choice.
If you've created a profile for an IDE that you think other students would
appreciate, we'd love to have you add the requisite profile files and
instructions to ide_profiles/. For example if you wanted to add a VS Code
profile, you'd add:

* /ide_profiles/vscode/.vscode
* /ide_profiles/vscode/README.md

The README should explain what the profile does, how to take advantage of it,
and how to install it.

Frankly, I've never been involved in a project with multiple IDE profiles
before. I believe the best way to handle this would be to keep them out of the
repo root to avoid clutter. My expectation is that most profiles will include
instructions to copy files to a new location to get picked up by the IDE, but
that's just a guess.

One last note here: regardless of the IDE used, every submitted project must
still be compilable with cmake and make./

## How to write a README
A well written README file can enhance your project and portfolio.  Develop your abilities to create professional README files by completing [this free course](https://www.udacity.com/course/writing-readmes--ud777).

