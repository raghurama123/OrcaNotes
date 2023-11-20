# 9. Check Convergence
## 9.1 Energy
```
-------------------------   --------------------
FINAL SINGLE POINT ENERGY       -76.320253607017
-------------------------   --------------------
```
- HF or DF
```
------------------------------------------------------
 DLPNO-MP2 CORRELATION ENERGY:      -0.240752652556 Eh
------------------------------------------------------
```
- DLPNO-MP2


## 9.2 Geometry
```
                    *****************************
                    * Geometry Optimization Run *
                    *****************************

Geometry optimization settings:
Update method            Update   .... BFGS
Choice of coordinates    CoordSys .... Z-matrix Internals
Initial Hessian          InHess   .... Almoef's Model

Convergence Tolerances:
Energy Change            TolE     ....  5.0000e-06 Eh
Max. Gradient            TolMAXG  ....  3.0000e-04 Eh/bohr
RMS Gradient             TolRMSG  ....  1.0000e-04 Eh/bohr
Max. Displacement        TolMAXD  ....  4.0000e-03 bohr
RMS Displacement         TolRMSD  ....  2.0000e-03 bohr
Strict Convergence                ....  False
```

```
                      .--------------------.
----------------------|Geometry convergence|-------------------------
Item                value                   Tolerance       Converged
---------------------------------------------------------------------
Energy change      -0.0000009421            0.0000050000      YES
RMS gradient        0.0000326782            0.0001000000      YES
MAX gradient        0.0001152425            0.0003000000      YES
RMS step            0.0007124988            0.0020000000      YES
MAX step            0.0017837746            0.0040000000      YES
........................................................
Max(Bonds)      0.0001      Max(Angles)    0.02
Max(Dihed)        0.10      Max(Improp)    0.00
---------------------------------------------------------------------

          ***********************HURRAY********************
          ***        THE OPTIMIZATION HAS CONVERGED     ***
          *************************************************
```
