# 6. Vibrational Frequencies

```
!wB97X-D3 RIJCOSX def2-TZVP def2/J TightSCF TightOpt Freq
```

## 6.1 Numerical Gradient and Hessian
```
!DLPNO-CCSD(T) cc-pVTZ cc-pVTZ/C OPT NUMGRAD NUMHESS
```

## 6.2 Restarting `NumFreq` calculations
```
!RI-B2PLYP DEF2-SVP DEF2-SVP/C NUMFREQ
%FREQ RESTART TRUE END
```
- If the basename.hess file is present on the same folder as the input, the computation will be restarted from where stopped.
