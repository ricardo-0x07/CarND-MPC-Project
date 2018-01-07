# Model Predictive Control Implementation


## The Model
- The State consists of:
    - Position (x, y), 
    - Orientation (psi), 
    - Velocity (v)), 
    - Cross Track Error (cte) is difference between the center of the road and the vehicles position,
    - Orientation Error (epsi)...
- Actuators for throttle (a) and steering (delta) are used to control the vehicles state. The t throttle and steering...
- State Update equations used the update the vehicles state resulting from actuator inputs:
    - *x~t+1~ = x~t~ + v~t~ * cos(psi~t~) * dt*
    - *y~t+1~ = y~t~ + v~t~ * sin(psi~t~) * dt*
    - *psi~t+1~ = psi~t~ + v~t~/Lf * delta * dt* Where Lf is distance of the vehicles center of gravity to the front.
    - *v~t+1~ = v~t~ + a * dt*
    - *cte~t+1~ = cte~t~ + v~t~ * sin(epsi~t~) * dt* Where the current Cross Track Error is the difference between the fitted polynomial reference line and the and the vehicles postions y: *cte~t~ = y~t~ - f(x~t~)*.
    - *epsi~t+1~ = epsi~t~ + v~t~/Lf * delta * dt* Where the current orientation error is the orientation of the desired trajectory subtracted from the the current vehicle orientation: *psi~t~ = psi~t~ - psides~t~*

## Timestep Length and Elapsed Duration (N & dt)


## Polynomial Fitting and MPC Preprocessing


## Model Predictive Control with Latency
