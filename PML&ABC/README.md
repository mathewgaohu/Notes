In wave propagations computation, we offen need to truncate an unbounded domain. 
However, an direct truncation will lead to reflections on the boundary when you use a Dirichlet boundary condition or Neumann boundary condition.

Usually we implement absorbing boundary condition (ABC) or perfectly matched layers (PML) to aviod reflection. 
Here is a paper which compares them, and shows how to implement them.
http://sourcedb.igg.cas.cn/cn/zjrck/201001/W020160519616038168413.pdf
@article{gao2017comparison,
  title={Comparison of artificial absorbing boundaries for acoustic wave equation modelling},
  author={Gao, Yingjie and Song, Hanjie and Zhang, Jinhai and Yao, Zhenxing},
  journal={Exploration Geophysics},
  volume={48},
  number={1},
  pages={76--93},
  year={2017},
  publisher={Taylor \& Francis}
}
