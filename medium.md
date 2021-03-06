## Medium Test for Randomized LP project

### I have implemented the Randomized Cutting Plane algorithm for solving LP program in C++
-> [commit link](https://github.com/vaithak/volume_approximation/commit/bb799d42d1e44049a2848ab4720d9468b9efb090)   
**Note:** I have implemented the alorithm from scratch but have used some part of previous PR's code and made some modifications for calculating an initial point in a polytope using log barrier method and gradient descent.  

### R interface along with the documentation
-> [commit link](https://github.com/vaithak/volume_approximation/commit/03544bc51584d80d24be5427e6e13d52f2061914)  
-> [pdf file of documentation](https://github.com/vaithak/GeomScale_LP/blob/master/randomized_lp_solver.pdf)  

### Test and it's result
```{r}
# computing Chebychev ball for a H-polytope (3d cube) P <- gen_cube(3, 'H')

row_norm <- sqrt(rowSums((P$A)^2))
P$A <- cbind(P$A, row_norm) 
var_bounds <- list("indices"=c(3), "lower"=c(0), "upper"=c(1000))  

randomized_lp_solver(P, obj=c(0,0,0,-1), bounds=var_bounds, algo=0)
```  
**Result:**  
```
$objective_value
[1] -0.9999

$variables
[1] 1.891452e-08 1.891452e-08 1.891452e-08 9.999000e-01
```   
**Therefore**  
**Center =** (1.891452e-08,  1.891452e-08,  1.891452e-08) and **Radius =** 0.9999.  
which is very close to the theoretical result:  
**Center =** (0, 0, 0) and **Radius =** 1.  

### Performance benchmarks
```
# P = gen_cube(10,'H')

Unit: milliseconds
                                  expr         min          lq         mean       median           uq        max  neval
 find_chebychev_ball_center_lpsolve(P)    1.865637    2.202339     2.438414     2.281963     2.578785   14.41695    100
 find_chebychev_ball_center_volesti(P) 1948.289957 2132.473352  2301.396565  2261.183982  2417.464725 3321.46584    100    
```  
