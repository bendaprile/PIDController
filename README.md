# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Reflection

**Describe the effect each of the P, I, D components had in your implementation.**

The Proportional term or P componenet of the PID controller adjusts the steering angle in proportion to a reference trajectory. In this case that reference trajectory is the center of the lane. There is a major problem with the P component in that it overshoots its trajectory. This creates an oscillation or a weave throughout the lane. If I set the P value to 1 and the I and D values to 0, the car would weave all around the lane. This is where the I and D values come into play.

The Differential term or D component of the PID controller is the derivative of CTE. It uses the cte and previous cte to allow the car to reach its reference trajectory more gracefully. This will help the weaving problem that the P term introduced, but it has a problem of its own. The differential term does not account for any systematic bias. An example of systematic bias can be if the steering wheels are permanently off center.

Finally, the Integral term or I component of the PID controller solves this problem. It solves the problem of systematic bias by using the sum of CTE over time. The controller will sometimes perform a bit worse and overshoot its reference trajectory a little with this component, but it will solve the problem of systematic bias which is very necessary.

**Describe how the final hyperparameters were chosen.**

Tuning my final hyperparameters took an immense amount of trial and error. I started out by tuning the P hyperparameter to see if I could get the car to stay in the lane at a slower speed. I then could see that the car stayed in its lane but was weaving all over the place. By increasing the value of the D hyperparameter I was able to get the car to more smoothly steer in its lane and not weave as much. I then realized that the car did not do great on straightaways and that the I hyperparameter might fix this. Increasing the I hyperparameter seemed to fix this.

In the end the car did not drive amazing so I spent some more time fidgeting with all of the hyperparameters together. After much fidgeting I decided that my implementation was as good as I would get it. In the future, I would like to try to implement twiddle and see if that will improve my implementation.


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

Fellow students have put together a guide to Windows set-up for the project [here](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/files/Kidnapped_Vehicle_Windows_Setup.pdf) if the environment you have set up for the Sensor Fusion projects does not work for this project. There's also an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3).

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

