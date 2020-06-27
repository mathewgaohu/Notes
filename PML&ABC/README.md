In wave propagations computation, we offen need to truncate an unbounded domain. 
However, an direct truncation will lead to reflections on the boundary when you use a Dirichlet boundary condition or Neumann boundary condition.

Usually we implement absorbing boundary condition (ABC) or perfectly matched layers (PML) to aviod reflection. 
Here is a paper which compares them, and shows how to implement them.

- Gao, Yingjie, Hanjie Song, Jinhai Zhang, and Zhenxing Yao. "Comparison of artificial absorbing boundaries for acoustic wave equation modelling." Exploration Geophysics 48, no. 1 (2017): 76-93.
http://sourcedb.igg.cas.cn/cn/zjrck/201001/W020160519616038168413.pdf
