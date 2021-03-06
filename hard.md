## Hard Test for Randomized LP project

### I have implemented the Simulated Annealing algorithm for solving LP program in C++
-> [commit link](https://github.com/vaithak/volume_approximation/commit/a8adb69249093ff96cf3c97f39ab6a18b880b05c)     
**Note:** For generating samples from distribution proportional to annealing function, I used the truncated exponential with implementation referenced from: [rexptr package](https://rdrr.io/cran/RGeode/src/R/rexptr.R)  

### R interface along with the documentation
-> [commit link](https://github.com/vaithak/volume_approximation/commit/03544bc51584d80d24be5427e6e13d52f2061914)  
-> [pdf file of documentation](https://github.com/vaithak/GeomScale_LP/blob/master/randomized_lp_solver.pdf)  

### Test and it's result
```{r}
# computing Chebychev ball for a H-polytope (3d cube) P <- gen_cube(3, 'H')

row_norm <- sqrt(rowSums((P$A)^2))
P$A <- cbind(P$A, row_norm) 
var_bounds <- list("indices"=c(3), "lower"=c(0), "upper"=c(1000))  

randomized_lp_solver(P, obj=c(0,0,0,-1), bounds=var_bounds, algo=1)
```  
**Result:**  
```
$objective_value
[1] -0.9994518914

$variables
[1] -0.0005430445  0.0005471988  0.0003732854 0.9994518914
```   
**Therefore**  
**Center =** (-0.0005430445, 0.0005471988, 0.0003732854) and **Radius =** 0.9994518914  
which is very close to the theoretical result:  
**Center =** (0, 0, 0) and **Radius =** 1.  

### Difficulties faced
  -)  In simulated annealing, many times the points generated on the chord in the polytope were very close to the polytope's boundary which due to numerical unstabiity caused the line_intersect method to fail, thus generating points outside the polytope. To counter this, I ensured the points generated by boltzmann distribution were a little off from the boundary.  
  
  -) The calculation of covariance matrix is a time intensive task therefore it's computation should be avoided until necessary. Currently I recalculate the covariance matrix in each phase but in future I would have to handle this to make it efficient.  
