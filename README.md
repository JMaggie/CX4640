---
Name: Maggie Jiang
Topic: 33 Accuracy and stability of different types of time-stepping methods. How they are derived and why they are what they are.
Title: Time Stepping Methods
---
# Time Stepping Method

## Table of Contents
- [Time Stepping Method]
- [Euler's Method](#Eulers-Method)
  	- [Accuracy](#Accuracy)
  	- [Stability](#Stability)
  	- [Derivation](#Derivation)
- [Runge-Kutta Methods](#Runge-Kutta-Methods)
  	- [Accuracy](#Accuracy)
  	- [Stability](#Stability)
  	- [Derivation](#Derivation)
  	- 
- [Sympletic Integrator](#Sympletic-Integrator)
- [Conclusion](#Conclusion)
- [References](#References)

## Time Stepping Methods

Time-stepping methods, also known as time integration methods or time-marching methods, are numerical techniques used to solve ordinary differential equations (ODEs) or partial differential equations (PDEs) that model dynamic systems evolving over time. These methods discretize the time domain into a sequence of time steps, updating the solution at each time step based on the information from the previous steps. Some of these methods include Euler's Method, Runge-Kutta Methods, Symplectic Methods, Leap-Frog Method, and Crank-Nicolson Method

## Explicit vs Implicit


## Euler's Method
Euler's method is the most common explicit method of evaluating ODEs [1]. Euler's method is first order [1]. A method is considered a "first-order method" if its rate of convergence or accuracy is proportional to the size of the discretization parameter raised to the first power. The order of a method is an indicator of how quickly the numerically computed solution approaches the true solution as the step size decreases. Euler's method is an s-step method, which is convergent [3]. In a convergent method, the numerically computed solution approaches the true solution as the step size approaches 0 [1]. A convergent method is consistent and stable [3]. 

Euler's method is a simple and straightforward method where the derivative at the current time step is used to estimate the value at the next time step. 
$$y_{n+1} = y_{n} + h f(t_n,y_n),$$ 
where $y_n$ is the numerical approximation of $y(t_n)$ at time $t_n$, $h$ is the time step size, and $f(t_n, y_n)$ is the slope of the solution at time $t_n$.

The method can be summarized in the following steps:

1. **Initialization:**
   - Start with the initial condition: $y_0$ at $t_0$.

2. **Iteration:**
   - At each time step $t_n$, use the update formula: $ y_{n+1} = y_n + h f(t_n, y_n) $
   - Move to the next time step: $t_{n+1} = t_n + h$.

3. **Repeat:**
   - Repeat the iteration until the desired endpoint or time is reached.

### Stability [2,3]
Euler's method is only conditionally stable. To be stable, the step size has to be very small. This can be seen when one observes a linear initial value problem, where $y'(t) = \lambda y(t)$ and $y(0) = y_0$. The solution to this problem is $y(t) = y_0 e^(\lambda t)$. However, if the initial conditions are changed from $y(0) = y_0$ to $y(0) = y_0 + \delta$, the solution becomes $y(t) = (y_0 + delta) e^(\lambda * t). The graph of $e^(x)$ is an exponential graph with a range of $(0, \inf)$. When $x = 0$, $e^x = 1$. When $x < 0$, $e^x < 1$. When $x > 0$, $e^x > 1$. Thus, when $\lambda <= 0$, a small change in the initial condition would only result in a small change in the solution, making the problem stable. On the contraty, when $\lambda > 0$, a small change in the initial solution would result in a largeg change in the solution, making the problem unstable. Thus, Euler's methos is conditionally stable. To determine how small the step size should be for Euler's method to be stable, we can make the following

For a given example with $\lambda < 0$, the to be stable, the growth factor would have to be constrained as such $\left| 1 + \lambda_{h} \right| < 1$ to account for amplification of error. One can see the  [1,3]

However, backwards euler's method also known as implicit euler's method is unconditionally stable. However, this is because

[3]

### Accuracy

Euler's method becomees more accurate as step size decreases [2], however, this would come with increasing computational cost. [2]

### Derivation
There are a few ways Euler's method may be derived. The first is by using numerical forward Euler's Method is known derived from the truncated Taylor's Expansion [1,2]. 
   
## Runge-Kutta Methods

These are a family of iterative methods that provide more accuracy than Euler's method. The most commonly used is the fourth-order Runge-Kutta method [4].

The general form of a Runge-Kutta method involves several stages of computation per time step. The fourth-order Runge-Kutta method (RK4) is widely applied due to its good balance between accuracy and computational efficiency. The RK4 method is defined by the following update formula for each time step:

1. **Stage 1:**
   \[ k_1 = h \cdot f(t_n, y_n) \]

2. **Stage 2:**
   \[ k_2 = h \cdot f(t_n + \frac{h}{2}, y_n + \frac{k_1}{2}) \]

3. **Stage 3:**
   \[ k_3 = h \cdot f(t_n + \frac{h}{2}, y_n + \frac{k_2}{2}) \]

4. **Stage 4:**
   \[ k_4 = h \cdot f(t_n + h, y_n + k_3) \]

5. **Update Formula:**
   \[ y_{n+1} = y_n + \frac{1}{6}(k_1 + 2k_2 + 2k_3 + k_4) \]

where $t_n$ is the current time, $y_n$ is the numerical approximation of the solution at time $t_n$, $h$ is the time step, and $f(t, y)$ is the derivative function specifying the ODE.

The RK4 method uses a weighted average of the four stages to update the numerical solution at each time step. The method is known for its accuracy and stability, and it is widely used in various applications.

There are other variants of the Runge-Kutta method with different orders (e.g., RK2, RK3), and the choice of method depends on the specific requirements of the problem and the desired trade-off between accuracy and computational cost.


### Accuracy

### Stability
The stability of the Runge-Kutta Method is also conditionally stable, like Euler's Method.

### Derivation
The derivation of Runge-Kutta Method can be seen by considering 

## Symplectic Methods

Symplectic methods or symphletic integrator (SI) are a class of numerical integration techniques specifically designed to preserve the symplectic structure of Hamiltonian systems in physics and mechanics [7]. Hamiltonian systems arise in classical mechanics, where they describe the motion of particles subject to conservative forces. The symplectic structure in these systems involves the preservation of certain geometric properties, such as phase space volume, which is crucial for capturing the qualitative behavior of the system accurately.

Symphletic integrator is a subclass of geometric integrator, which is a numerical method designed to preserve the geometric properties associated with the true solution to a differential equation [8].

## Leapfrog Method
This is a symplectic integrator often used in physics simulations. It alternates between updating positions and velocities, which can provide good long-term stability for certain systems.

The leapfrog method is symphletic and has a global stability [6]

## Adams-Bashforth and Adams-Moulton Methods
These are explicit methods that use past values to predict future values. They are often used for solving ordinary differential equations.

## Backward Differentiation Formula Methods

## Richardson Extrapolation

## Conclusion

## References
1. Euler's Method. (October 5, 2023). In Wikipedia. https://en.wikipedia.org/wiki/Euler_method#:~:text=In%20mathematics%20and%20computational%20science,with%20a%20given%20initial%20value.
2. Zeltkevic, M. (1998) Massachusetts Institute of Technology. https://web.mit.edu/10.001/Web/Course_Notes/Differential_Equations_Notes/node3.html
3. Illinois Institute of Technology. (n.d). Chapter 4: Stiffness and Stability. http://www.math.iit.edu/~fass/478578_Chapter_4.pdf. 
4. https://en.wikipedia.org/wiki/Runge%E2%80%93Kutta_methods
5. https://www.sciencedirect.com/topics/mathematics/runge-kutta-method
6. https://young.physics.ucsc.edu/115/leapfrog.pdf
7. https://en.wikipedia.org/wiki/Symplectic_integrator
8. https://en.wikipedia.org/wiki/Geometric_integrator
