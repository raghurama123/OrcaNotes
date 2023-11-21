# 10. Transition State Search

## 10.1 Nudged Elastic Band

Here is an example input for HCN - HNC isomerization reaction

```
!B3LYP DEF2-SVP D4 NEB-TS FREQ

%NEB 
  NEB_END_XYZFILE "HNC.xyz"
  NEB_TS_XYZFILE  "TS.xyz"
  PREOPT_ENDS     TRUE
END

%GEOM
  CALC_HESS       TRUE
  RECALC_HESS     5
  MAXITER         50
END

%MAXCORE 4000

%PAL
  NPROCS 8
END

* XYZfile 0 1 HCN.xyz
```

Here are the geometries used

### HCN.xyz
```
3
HCN
C         -2.76788        0.86239        0.00000
N         -1.61084        0.87791        0.00000
H         -3.82622        0.84820        0.00000
```

### HNC.xyz 
```
3
HNC
C         -2.76788        0.86239        0.00000
N         -1.61084        0.87791        0.00000
H         -0.53913        0.93704       -0.00000
```
### TS.xyz 
```
3
TS
C         -2.76788        0.86239        0.00000
N         -1.61084        0.87791        0.00000
H         -2.29372        1.98091       -0.00000
```

### Output
- Energy
```
---------------------------------------------------------------
                      PATH SUMMARY FOR NEB-TS             
---------------------------------------------------------------
All forces in Eh/Bohr. Global forces for TS.

Image     E(Eh)   dE(kcal/mol)  max(|Fp|)  RMS(Fp)
  0     -93.30152     0.00       0.00001   0.00001
  1     -93.26819    20.92       0.00177   0.00090
  2     -93.24438    35.85       0.00252   0.00147
  3     -93.22971    45.06       0.00867   0.00564
  4     -93.22535    47.80       0.00028   0.00015 <= CI
 TS     -93.22535    47.80       0.00007   0.00004 <= TS
  5     -93.23119    44.13       0.00452   0.00248
  6     -93.24124    37.82       0.00205   0.00118
  7     -93.25247    30.78       0.00104   0.00055
  8     -93.26687    21.75       0.00217   0.00096
  9     -93.27982    13.62       0.00011   0.00004
```
- Frequencies
```
-----------------------
VIBRATIONAL FREQUENCIES
-----------------------

Scaling factor for frequencies =  1.000000000  (already applied!)

   0:         0.00 cm**-1
   1:         0.00 cm**-1
   2:         0.00 cm**-1
   3:         0.00 cm**-1
   4:         0.00 cm**-1
   5:         0.00 cm**-1
   6:     -1130.57 cm**-1 ***imaginary mode***
   7:      2089.81 cm**-1
   8:      2621.95 cm**-1
```

## 10.2 OptTS

Following NEB, one can do a tight optimization of the TS structure
```
!B3LYP DEF2-SVP D4 OptTS FREQ TightSCF

* XYZfile 0 1 TS_NEB_NEB-TS_converged.xyz

%GEOM
  CALC_HESS       TRUE
  RECALC_HESS     5
  MAXITER         50
  CONVERGENCE     Tight
END

%MAXCORE 4000

%PAL
  NPROCS 8
END
```

- Frequencies
```
-----------------------
VIBRATIONAL FREQUENCIES
-----------------------

Scaling factor for frequencies =  1.000000000  (already applied!)

   0:         0.00 cm**-1
   1:         0.00 cm**-1
   2:         0.00 cm**-1
   3:         0.00 cm**-1
   4:         0.00 cm**-1
   5:         0.00 cm**-1
   6:     -1130.55 cm**-1 ***imaginary mode***
   7:      2089.82 cm**-1
   8:      2621.93 cm**-1
```

