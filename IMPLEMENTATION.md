# Model Predictive Control Implementation


## The Model

- The State consists of:
  - Position (x, y), 
  - Orientation (psi), 
  - Velocity (v)), 
  - Cross Track Error (cte) is difference between the center of the road and the vehicles position,
  - Orientation Error (epsi)...
- Actuators for throttle (a) and steering (delta) are used to control the vehicles state. The the throttle and steering actuator were constrained to +/-1 (-1 max breaking and + 1 max acceleration) and +/-25 degrees (steering angle) respectively.
- State Update equations used the update the vehicles state resulting from actuator inputs:
    - *x~t+1~ = x~t~ + v~t~ * cos(psi~t~) * dt*
    - *y~t+1~ = y~t~ + v~t~ * sin(psi~t~) * dt*
    - *psi~t+1~ = psi~t~ + v~t~/Lf * delta * dt* Where Lf is distance of the vehicles center of gravity to the front.
    - *v~t+1~ = v~t~ + a * dt*
    - *cte~t+1~ = cte~t~ + v~t~ * sin(epsi~t~) * dt* Where the current Cross Track Error is the difference between the fitted polynomial reference line and the and the vehicles postions y: *cte~t~ = y~t~ - f(x~t~)*.
    - *epsi~t+1~ = epsi~t~ + v~t~/Lf * delta * dt* Where the current orientation error is the orientation of the desired trajectory subtracted from the the current vehicle orientation: *psi~t~ = psi~t~ - psides~t~*

## Timestep Length and Elapsed Duration (N & dt):

- I first decided that the horizon T should one to two seconds.
- Then duration between actuations was tunned until car was observed to be responsive enough. The Initial value used was 0.01 this resulted in instability in the car, oscillating from one side of the road to the next which was reduced after the increasing this value. This value was increased until this oscillation was reduced to a satisfactory level.
- Then the value for the number of time steps was keep within the desired horizon range of one to two seconds. Based on the desired horizon range of one to two seconds the value would start at one second divided by the established duration between actuations of 5 (20 steps) and adjust to a maximum value that avoided responsiveness issues.


## Polynomial Fitting and MPC Preprocessing

- A transform is done to the state position and orientation to get the car in the same orientation of the line to help simplify to polynomial fit process.

## Model Predictive Control with Latency

- The 100ms of **latency** is used in the state update equations, it is substituted for dt in the above equation, to recompute the state values in anticipation of 100ms of **latency**. Note the steering and throttle values provided by the simulation are used of *delta* and *a* assuming that that should be about the same.
