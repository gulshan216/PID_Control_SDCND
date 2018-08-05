# PID Control Project

The purpose of the project is to implement a PID controller and tune the PID hyperparameters to maneuver the vehicle around a track in the simulator.
The PID controller must respond with steering and throttle commands to drive the car reliably around the simulator track.
The simulator will provides the cross track error (CTE) and the velocity (mph) in order to compute the appropriate steering angle.

## Rubric Discussion Points
* Describe the effect each of the P, I, D components had in your implementation. 

The P component had as expected a proportional effect on the steering of the car based on the cross track error. 
But only using the P component, the vehicle always overshooted the reference line and hence the car was wobbling around a lot in the simulator.

Adding the I component was supposed to help overcome the systematic bias problem. 
But for the car in the simulator, adding the I component did not have much effect.

The D component helped a lot in keeping the car in the center of the lane as much possible as it counteracted the effect of the car overshooting the reference line.

* Describe how the final hyperparameters were chosen.

The parameters were tuned by performing some manual twiddling. Initially I started with the values of P,I,D coefficients set to 1,0,0 to just check the effect of the proportional component.
As expected the car overshooted the reference line and went to the non-drivable part of the track.
Then to turn down the effect of the proportional component i tuned the value of P component to 0.3. 
Then i basically added the D-component to reduce the ringing effect of the car and set the parameters to 0.3,0,1.0.
This reduced the ringing effect a bit but still not by a lot. So as we do in twiddle i first increased the value of D-component by 1 and set the parameters to 0.3,0,2.0
This significantly reduced the ringing effect and so i incremented the value of D-component by 1 again and set the parameters to 0.3,0,3.0 to see the effect. 
And the total error reduced again but incrementing Kd any further did not improve the performance.
Now tried adding the I-component by setting the parameters to 0.3,1.0,3.0. This had a very adverse effect on the total error.
I had to tune down the parameter a lot to get the performance similar to just the PD-controller. I ended up tuning the I-parameter as low as 0.001.
The performance mainly improved on turns. Hence my final set of chosen hyperparameters were 0.3,0.001,3.0 

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

