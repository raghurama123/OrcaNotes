# 12. Excited State Dynamics

- We will follow Orca 5.0.4 Manual, "Section 8.15: Excited State Dynamics", pages 394-414.
- Also see "Section 9.38: Simulation and Fit of Vibronic Structure in Electronic Spectra, Resonance Raman Excitation Profiles and Spectra with the `ORCA_ASA` Program"
- Also see "Section 9.39 More on the Excited State Dynamics module" for full list of keywords for `ORCA_ESD`

## 12.1 Absorption spectrum of Benzene using the ideal model, Adiabatic Hessian (AH)
- Let's predict the absorption spectrum of benzene, which has one band above 220 nm correponding to a symmetry forbidden excitation to the S1 state. 
 
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
  NPROCS 16
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
  NPROCS 16
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

### 12.1.3 `ESD (ABS)`
- Since the first transition of benzene is symmetry forbidden with a tiny oscillator strength ($\thickapprox 10^{-6}$ or less) and thus all the intensity comes from vibronic coupling (HT effect). So, we have to set `DOHT TRUE` in the ESD calculation. In molecules with strongly allowed transitions that usually can be left as FALSE (the default). 
```
!wB97X-D3 RIJCOSX DEF2-SVP  DEF2/J TIGHTSCF ESD(ABS) XYZFILE

%BASE "esd"

*XYZFILE 0 1 s0.xyz

%MAXCORE 64000

%SCF
  MAXITER 150
END

%PAL
  NPROCS 16
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

### 12.1.4 `ESD (FLUOR)`
```
!wB97X-D3 RIJCOSX DEF2-SVP  DEF2/J TIGHTSCF ESD(FLUOR) XYZFILE

%BASE "esd_flu"

*XYZFILE 0 1 s0.xyz

%MAXCORE 64000

%SCF
  MAXITER 150
END

%PAL
  NPROCS 16
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
  LINES           VOIGT
  LINEW           75
  INLINEW         200
END
```
- NOTE: For plotting absorption and emission spectrum together, one has to normalize both the plots as done in [https://doi.org/10.1063/1.5010895](https://doi.org/10.1063/1.5010895).   
- Fluoroescence rate constant is printed in the output
```
          ***Everything is set, now computing the correlation function***

Homogeneous linewidth is:                       75.00 cm-1
Inhomogeneous linewidth is:                     200.00 cm-1
Number of points:                               65536
Maximum time:                                   1061.77 fs
Spectral resolution:                            5.00 cm-1
Temperature used:                               298.15 K
Z value:                                        1.703696e-44
Cutoff for the correlation function:            1.00e-06
Adiabatic energy difference:                    44188.52 cm-1
0-0 energy difference:                          43045.64 cm-1
Reference transition dipole (x,y,z):            (-0.00420 0.00000),
                                                (0.00290 0.00000),
                                                (0.00001 0.00000) 
Calculating correlation function:               ...done
Last element of the correlation function:       0.000000,0.000000
Computing the Fourier Transform:                ...done

The calculated fluorescence rate constant is    2.043006e+07 s-1          <----- HERE
with 0.02% from FC and 99.98% from HT

The fluorescence spectrum was saved in          esd_flu.spectrum

Total run time: 0 hours 6 minutes 49 seconds
```
