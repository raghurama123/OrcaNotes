# 12. Excited State Dynamics

- We will follow Orca 5.0.4 Manual, "Section 8.15: Excited State Dynamics", pages 394-414.
- A related section is "Section 9.38: Simulation and Fit of Vibronic Structure in Electronic Spectra, Resonance Raman Excitation Profiles and Spectra with the `ORCA_ASA` Program"

## 12.1 Absorption spectrum of Benzene using the ideal model, Adiabatic Hessian (AH)

### 12.1.1 S0 state `OPT` and `FREQ`
```
!wB97X-D3 RIJCOSX DEF2-SVP  DEF2/J TIGHTSCF TIGHTOPT FREQ XYZFILE

%BASE "s0"

*XYZFILE 0 1 geom_UFF.xyz

%MAXCORE 64000

%SCF
  MAXITER 150
END

%PAL
  PROCS 16
END

%GEOM
  CALC_HESS TRUE
  RECALC_HESS 5
  MAXITER 50
END
```

* `geom_UFF.xyz`
```
12
benzene
C        1.38212000       -0.21688000        0.00497000
C        0.50328000       -1.30535000       -0.00923000
C       -0.87883000       -1.08847000       -0.01427000
C       -1.38212000        0.21688000       -0.00497000
C       -0.50328000        1.30535000        0.00930000
C        0.87883000        1.08847000        0.01420000
H        2.45137000       -0.38467000        0.00882000
H        0.89264000       -2.31521000       -0.01633000
H       -1.55873000       -1.93054000       -0.02535000
H       -2.45137000        0.38467000       -0.00882000
H       -0.89264000        2.31520000        0.01653000
H        1.55873000        1.93054000        0.02515000
```

### 12.1.2 S1 state `OPT` and `FREQ`
```
!wB97X-D3 RIJCOSX DEF2-SVP  DEF2/J TIGHTSCF TIGHTOPT FREQ XYZFILE

%BASE "s1"

*XYZFILE 0 1 s0.xyz

%MAXCORE 64000

%SCF
  MAXITER 150
END

%PAL
  PROCS 16
END

%GEOM
  CALC_HESS   TRUE
  RECALC_HESS 5
  MAXITER     50
END

%TDDFT
 NROOTS       5
 IROOT        1
 TDA          FALSE
 TRIPLETS     FALSE
END
```

### 12.1.3 `ESD`
```
!wB97X-D3 RIJCOSX DEF2-SVP  DEF2/J TIGHTSCF ESD(ABS) XYZFILE

%BASE "s1"

*XYZFILE 0 1 s0.xyz

%MAXCORE 64000

%SCF
  MAXITER 150
END

%PAL
  PROCS 16
END

%TDDFT
 NROOTS       5
 IROOT        1
 TDA          FALSE
 TRIPLETS     FALSE
END

%ESD GSHESSIAN "s0.hess"
  ESHESSIAN    "s1.hess"
  DOHT TRUE
END
```
