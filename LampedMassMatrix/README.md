When we try to use explicit propagation in FEniCS, we need to use lamped mass matrix (diagonal matrix), otherwise we will always have to solve linear systems in each loop.

