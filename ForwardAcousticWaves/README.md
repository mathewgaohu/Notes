I want to implement a forward acoustic wave propagation in an half 2D plane.

$$ \frac{1}{\kappa} p_{tt} - \nabla \cdot (\frac{1}{\rho} \nabla p) = source(x,z,t) $$

The easiest way might be directly applying a test function and propagating it.

reference:

- This is a toturial of acoustic waves with FEM. It is not FEniCS but the theoretical ideas are helpful.
https://www.dealii.org/developer/doxygen/deal.II/step_23.html

-
