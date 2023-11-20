# 5. Geometry Optimization
```
!wB97X-D3 RIJCOSX def2-TZVP def2/J TightSCF TightOpt 
```
- `TightSCF` and `TightOpt` for tight convergence criteria for SCF convergence and geometry convergence

## 5.1 Calculate Hessian
```
%geom
  Calc_Hess true
  Recalc_Hess 5
  MaxIter 50
end
```

## 5.2 Numerical Gradient
```
!DLPNO-CCSD(T) cc-pVTZ cc-pVTZ/C OPT NUMGRAD
```
