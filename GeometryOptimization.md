# 5. Geometry Optimization
```
!WB97X-D3 RIJCOSX DEF2-TZVP DEF2/J TIGHTSCF TIGHTOPT 
```
- `TIGHTSCF` and `TIGHTOPT` for tight convergence criteria for SCF convergence and geometry convergence

## 5.1 Calculate Hessian
```
%GEOM
  CALC_HESS TRUE
  RECALC_HESS 5
  MAXITER 50
END
```

## 5.2 Numerical Gradient
```
!DLPNO-CCSD(T) CC-PVTZ CC-PVTZ/C OPT NUMGRAD
```

## 5.3 Convergence criteria

### `LOOSEOPT`
```
Energy Change            TolE     ....  3.0000e-05 Eh
Max. Gradient            TolMAXG  ....  2.0000e-03 Eh/bohr
RMS Gradient             TolRMSG  ....  5.0000e-04 Eh/bohr
Max. Displacement        TolMAXD  ....  1.0000e-02 bohr
RMS Displacement         TolRMSD  ....  7.0000e-03 bohr
```

### `NORMALOPT`
```
Energy Change            TolE     ....  5.0000e-06 Eh
Max. Gradient            TolMAXG  ....  3.0000e-04 Eh/bohr
RMS Gradient             TolRMSG  ....  1.0000e-04 Eh/bohr
Max. Displacement        TolMAXD  ....  4.0000e-03 bohr
RMS Displacement         TolRMSD  ....  2.0000e-03 bohr
```

### `TIGHTOPT`
```
Energy Change            TolE     ....  1.0000e-06 Eh
Max. Gradient            TolMAXG  ....  1.0000e-04 Eh/bohr
RMS Gradient             TolRMSG  ....  3.0000e-05 Eh/bohr
Max. Displacement        TolMAXD  ....  1.0000e-03 bohr
RMS Displacement         TolRMSD  ....  6.0000e-04 bohr
```

### `VERYTIGHTOPT`
```
Energy Change            TolE     ....  2.0000e-07 Eh
Max. Gradient            TolMAXG  ....  3.0000e-05 Eh/bohr
RMS Gradient             TolRMSG  ....  8.0000e-06 Eh/bohr
Max. Displacement        TolMAXD  ....  2.0000e-04 bohr
RMS Displacement         TolRMSD  ....  1.0000e-04 bohr
```
