Now how to implement GLL in fenics. 

First we need Legendre basis on an element. 
Then we build a form. like
a = u*v*dx,
then we assemble it to a matrix
A = assemble(a). 

Here it is, how to apply Gauss-Lobatto quadrature in the assembling. 

I check the document of assemble, it accepts 
form_compiler_parameters={'quadrature_scheme': 'vertex',
                                          'quadrature_degree': 1}).
But nothing lead to the quadrature created by FIAT.


reference:
- FIAT package has something called GLL FiniteElement, which is only for 1D. The question is I don't know how to use it even in 1D.
https://github.com/FEniCS/fiat/blob/master/FIAT/gauss_lobatto_legendre.py

- (continued) and a quadrature rule called GLL Quadrature.
https://github.com/FEniCS/fiat/blob/master/FIAT/quadrature.py

- (continued) and here is a test for GLL. You can see how the functions are used.
https://github.com/FEniCS/fiat/blob/master/test/unit/test_gauss_lobatto_legendre.py

- FIAT has 'UFCQuadrilateral' 
https://github.com/FEniCS/fiat/blob/master/FIAT/reference_element.py

- You can see what they accept in 'assemble'
https://fenics.readthedocs.io/projects/ffc/en/latest/_modules/ffc/parameters.html

- People talked about how to apply arbitrary quadrature.
https://bitbucket.org/fenics-project/dolfin/issues/955/support-for-arbitrary-quadrature-rules

- Someone suggested vertex scheme, but I didn't see any difference. 
https://fenicsproject.org/qa/655/question-about-quadratures-rules/

- You can see FEniCS sources here. 
https://bitbucket.org/fenics-project/

- You can tensorize two finite elements.
https://github.com/FEniCS/fiat/blob/master/FIAT/tensor_product.py

- Look at the source code. 
- UFL actually support GLL element. 
https://bitbucket.org/fenics-project/ufl/src/master/ufl/finiteelement/elementlist.py
- (continued) but when we build a function space. The error occurs since 'ffc' says it doesn't support 'GLL' family. We can see that 'fiat' supports GLL.
https://bitbucket.org/fenics-project/ffc/src/master/ffc/fiatinterface.py
- (continued) I changed 'ffc's supported list and then we can build the function space.

- The next question is how to apply lobatto quadrature. The default scheme doesn't generate diagonal matrix.


