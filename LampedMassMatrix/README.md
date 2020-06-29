When we try to use explicit propagation in FEniCS, we need to use lamped mass matrix (diagonal matrix), otherwise we will always have to solve linear systems in each loop.

1. An easiest way is summing the rows of the matrix. However it only works in P1 elements. (Though I don't understand why it works.)
2. An anvanced way is to use Gauss-Lobatto points and compute the integral with Gauss-Lobatto quadrature. In this setting the mass matrix will automatically be diagonal (or approximately diagonal). This is what I am looking for. But how to apply it in FEniCS?
3. Another way seems to be scalling. 

Based on the references I found, there is no direct way to implement GLL on 2D quadrilateral meshes. But it shouldn't be too hard. I found a file 'quadrature_schemes.py' in FIAT, where it use 'ref_el.product' to deal with quadrilaterals. I guess it tensorize the 1D scheme. I need to check it and then the problem is reduced to finding GLL for 1D, which I think is already there.

reference:
- Three ways to lamp the mass matrix.
https://scicomp.stackexchange.com/questions/19704/how-to-formulate-lumped-mass-matrix-in-fem/19714

- How to lamp a matrix. Examples of P1 and P2 elements.
https://comet-fenics.readthedocs.io/en/latest/demo/tips_and_tricks/mass_lumping.html

- (continued) In P2 case, how to integrate with vertex quadrature. 
https://comet-fenics.readthedocs.io/en/latest/_downloads/599fd05ffe9168f05cd5074a2c69391f/lumping_scheme.py

- The Ch.16 of a book is mentioned.
https://www.sciencedirect.com/book/9780750664318/the-finite-element-method-set

- An note about the mass matrix for Gauss-Lobatto nodes. (looks like a proof.)
https://authors.library.caltech.edu/86801/2/1412.2276.pdf

- A chapter describing lamping mass matrix.
http://kis.tu.kielce.pl/mo/COLORADO_FEM/colorado/IFEM.Ch31.pdf

- The FIAT package has GLL function but only works for 1D.
https://github.com/FEniCS/fiat/blob/master/FIAT/gauss_lobatto_legendre.py

- In 2016 some people discussed about GLL in fenics FIAT. 
https://bitbucket.org/fenics-project/fiat/issues/14/gauss-legendre-lobatto-points-used-for-the
- (continued) David Ham write GLL and merged it into the master branch. And they disscussed about naming the function. So I think there exists a function to set the Lobatto points and a function to implement the Gauss-Lobatto quadrature.
https://bitbucket.org/fenics-project/ufl/pull-requests/63/add-gl-and-gll-to-the-element-lists/diff

- A paper. It mentioned some papers working on the mass-lamping elements. And it says in 2D cases we need to use ’tensorization’ of a 1D finite element, tensorized Gauss-Lobatto points combined with Lagrange Qk isoparametric elements.
http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.405.7100&rep=rep1&type=pdf

- The 74 and 76 page of this book talks about explicit method and lumping mass. But it only mentions 1D 1order case.
http://people.cs.uchicago.edu/~ridg/scicomp17/iamuf.pdf


