For the error function, we can see that there's no significant change when n > 50
Thats the reason I chose n = 100 in the project.

import numpy as np
import matplotlib.pyplot as plt
from scipy.special import erfc

L = 0.04  
v = 0.000217  
U0 = 40  
dy = 0.001 
jm = int(L/dy + 1) 
y = np.linspace(0, L, jm) 
t = 1.08
eta = y / (2 * np.sqrt(v * t))
eta1 = L / (2 * np.sqrt(v * t))  

u_analytical_1 = U0 * sum(erfc(2*n*eta1 + eta) - erfc(2*(n+1)*eta1 - eta) for n in range(100))

u_analytical_2 = U0 * sum(erfc(2*n*eta1 + eta) - erfc(2*(n+1)*eta1 - eta) for n in range(50))

u_analytical_3 = U0 * sum(erfc(2*n*eta1 + eta) - erfc(2*(n+1)*eta1 - eta) for n in range(25))

u_analytical_4 = U0 * sum(erfc(2*n*eta1 + eta) - erfc(2*(n+1)*eta1 - eta) for n in range(1))


gap_1 = u_analytical_1 - u_analytical_2
gap_2 = u_analytical_2 - u_analytical_3
gap_3 = u_analytical_3 - u_analytical_4

plt.figure(figsize=(10, 6))
plt.plot(y, gap_1, label='Gap between 100 and 50 terms')
plt.plot(y, gap_2, label='Gap between 50 and 25 terms')
plt.plot(y, gap_3, label='Gap between 25 and 1 terms')
plt.xlabel('Position (m)')
plt.ylabel('Error')
plt.legend()
plt.grid(True)
plt.show()
