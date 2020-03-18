## Hard Test for Randomized LP project

### I have implemented the Simulated Annealing algorithm for solving LP program in C++
-> commit link   

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

### Difficulties faced
