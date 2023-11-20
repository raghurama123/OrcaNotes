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

## 5.3 Convergence criteria

### `LooseOpt`
```
Energy Change            TolE     ....  3.0000e-05 Eh
Max. Gradient            TolMAXG  ....  2.0000e-03 Eh/bohr
RMS Gradient             TolRMSG  ....  5.0000e-04 Eh/bohr
Max. Displacement        TolMAXD  ....  1.0000e-02 bohr
RMS Displacement         TolRMSD  ....  7.0000e-03 bohr
```

### `NormalOpt`
```
Energy Change            TolE     ....  5.0000e-06 Eh
Max. Gradient            TolMAXG  ....  3.0000e-04 Eh/bohr
RMS Gradient             TolRMSG  ....  1.0000e-04 Eh/bohr
Max. Displacement        TolMAXD  ....  4.0000e-03 bohr
RMS Displacement         TolRMSD  ....  2.0000e-03 bohr
```

### `TightOpt`
```
Energy Change            TolE     ....  1.0000e-06 Eh
Max. Gradient            TolMAXG  ....  1.0000e-04 Eh/bohr
RMS Gradient             TolRMSG  ....  3.0000e-05 Eh/bohr
Max. Displacement        TolMAXD  ....  1.0000e-03 bohr
RMS Displacement         TolRMSD  ....  6.0000e-04 bohr
```

### `VeryTightOpt`
```
Energy Change            TolE     ....  2.0000e-07 Eh
Max. Gradient            TolMAXG  ....  3.0000e-05 Eh/bohr
RMS Gradient             TolRMSG  ....  8.0000e-06 Eh/bohr
Max. Displacement        TolMAXD  ....  2.0000e-04 bohr
RMS Displacement         TolRMSD  ....  1.0000e-04 bohr
```
