# Hilber-Hughes-Taylor (HHT) Time Integration Verification

## Problem Statement and Results

In this one element test, the base and top of the 2D element is fixed in y
direction. An acceleration is prescribed at the base of the element in the x direction.

HHT time integration is used to obtain the displacement, velocity and acceleration
at the top of the element. The equation of motion is

\begin{equation}
\mathbf{M} a_x(t + \delta t) + \mathbf{K}((1+\alpha)d_x(t+\delta t) - \alpha d_x(t)) = 0,
\end{equation}
the $a_x$ and  $d_x$ are column vectors that contain the acceleration and displacement in the
x-direction of the top and bottom node, respectively. The row of the mass matrix ($\textbf{M}$) that
corresponds to the top node is computed as $\rho \cdot A \cdot l \cdot [1/3\, 1/6]$, where $\rho$ is
the density, $A$ is the area, and $l$ is the length. The row of the stiffness matrix that
corresponds to the top node is $E\cdot A\cdot l \cdot [1\,-1]$, where $E$ is Young's modulus.

Solving the above equation analytically for $\alpha = -0.3$, $\beta = 0.4225$, and
$\gamma = 0.8$ gives the results in [hht-disp-vel-accel]. The interactive results shown in
[verification_figure] compare the analytical result ("previous") with the result computed
from MASTODON for this problem ("current").

!table id=hht-disp-vel-accel caption=Analytical displacement, acceleration, and velocity in the x-direction.
| t | Displacement | Velocity | Acceleration |
| - | - | - | - |
| 0 | 0    | 0   |  0 |
| 1 | 0.25 | 0.473 | 0.591 |
| 2 | 0.871| 0.785 | 0.241 |
| 3 | 1.467 | 0.439 | -0.493 |

!plot scatter filename=test/tests/kernels/time_integration/gold/hht_out.csv
              data=[{'x':'time', 'y':'accel_x', 'name':'Acceleration'},
                    {'x':'time', 'y':'disp_x', 'name':'Displacement'},
                    {'x':'time', 'y':'vel_x', 'name':'Velocity'}]
              layout={'xaxis':{'title':'Time (sec)'},
                      'yaxis':{'title':'Acceleration (g)'},
                      'title':'Acceleration history'}
              caption=Acceleration, velocity and displacement values computed using HHT integration in MASTODON
              id=verification_figure


## Complete Input File

!listing test/tests/kernels/time_integration/hht.i start=[Mesh]
