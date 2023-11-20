# 6. Vibrational Frequencies

```
!WB97X-D3 RIJCOSX DEF2-TZVP DEF2/J TIGHTSCF TIGHTOPT FREQ
```

## 6.1 Numerical Gradient and Hessian
```
!DLPNO-CCSD(T) CC-PVTZ CC-PVTZ/C OPT NUMGRAD NUMHESS
```

## 6.2 Restarting `NumFreq` calculations
```
!RI-B2PLYP DEF2-SVP DEF2-SVP/C NUMFREQ
%FREQ
  RESTART TRUE
END
```
- If the basename.hess file is present on the same folder as the input, the computation will be restarted from where stopped.
