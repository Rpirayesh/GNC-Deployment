# GNC-Deployment
Taske: take the CSD 3U 2-spring data from the CSD datasheet (data in code) and derive the equivalent spring parameters k and b such that the mass-spring-damper model can accurately predict the ejection velocity of the dispenser for the range of spacecraft (payload) masses from 3kg to 15kg. 

This code is designed to solve a common physics problem: finding the parameters of a spring-mass-damper system given some measurements of the velocities of the masses.

    First, the masses and corresponding velocities are recorded as numpy arrays. These represent the real data of the system, with each pair of corresponding mass-velocity values indicating a measurement.

    The differential equation that governs the behavior of the spring-mass-damper system is defined. This equation is derived from Newton's second law of motion, and describes how the velocity and displacement of the mass change over time due to the forces exerted by the spring and the damper.

    To numerically solve the differential equation, the Runge-Kutta 4th order method is used. This method is a common algorithm for approximating the solutions to ordinary differential equations, and is more accurate than simpler methods like Euler's method. The method is implemented in the runge_kutta_4th_order function, which performs a single update of the state (displacement and velocity) given the current state and the time step.

    The solve_differential_equation function uses the Runge-Kutta method to simulate the system over a period of time. It starts with an initial state and applies the Runge-Kutta method iteratively to find the state at each point in time.

    The goal of the code is to find the parameters of the spring and damper (the spring constant k and the damping coefficient b) that best fit the observed data. To do this, an objective function (or "loss function") is defined, which quantifies how well the simulation matches the data. The loss function is the sum of squared differences between the velocities predicted by the simulation and the actual velocities. This is a common choice of loss function in regression problems, as it penalizes larger errors more heavily and is differentiable.

    Finally, the scipy.optimize.minimize function is used to find the values of k and b that minimize the loss function. The Nelder-Mead method is used, which is a simple optimization algorithm that does not require the computation of derivatives.

After running the optimization, the optimized parameters are printed out.

The key to this solution was the careful selection of the numerical method (the 4th order Runge-Kutta method) for solving the differential equation. The 4th order Runge-Kutta method is accurate enough to capture the behavior of the system, while also being relatively easy to implement and computationally efficient. Using a less accurate method (like Euler's method) might have led to larger errors in the simulation, making it harder to find the correct parameters.

Another critical aspect was the formulation of the objective function and the choice of optimization algorithm. By formulating the problem as a regression problem and using a sum of squares loss function, the optimization problem could be solved efficiently using standard algorithms.
