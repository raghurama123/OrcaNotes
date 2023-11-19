# Orca usage notes

# 1. Input/Output control

## 1.1 Basis Input

```
!HF DEF2-SVP
* xyz 0 1
O         -3.56626        1.77639        0.00000
H         -2.59626        1.77639        0.00000
H         -3.88959        1.36040       -0.81444
*
```
## 1.2 Read geometry from a file

```
!HF DEF2-SVP 
* xyz 0 1 geom_init.xyz
```
where `geom_init.xyz` contains

```
3
test
O         -3.56626        1.77639        0.00000
H         -2.59626        1.77639        0.00000
H         -3.88959        1.36040       -0.81444
*
```
## 1.3 Store final geometry in a file

```
!HF DEF2-SVP Opt XYZFILE
* xyz 0 1 geom_init.xyz
```
- If the input file is test.com, the final geometry will be stored in the file `test.xyz`

## 1.4 Change basename
```
!HF DEF2-SVP Opt XYZFILE
%base "HF_SVP"
* xyz 0 1 geom_init.xyz
```
- If the input file is test.com, the final geometry will be stored in the file `HF_SVP.xyz`. All the files, expect the output file will have the basename "HF_SVP"

# 2. Memory and cores
```
%MaxCore 4000

%pal nprocs 8
end
```
- 4GB per core and 8 cores for this calculation.

## 2.1 Optimal memory for helios

- `%MaxCore 4000` qa, qb
- `%MaxCore 5000` qd
- `%MaxCore 14000` q
- `%MaxCore 16000` qc


# 3. Methods
```
!HF DEF2-SVP
```
- HF
```
!RI-MP2 cc-pVTZ cc-pVTZ/C
```
- RI-MP2
```
!DLPNO-MP2 cc-pVTZ cc-pVTZ/C
```
- DLPNO-MP2
  
# 4. Single Point Energy

## 4.1 SCF Convergence

```
!wB97X-D3 RIJCOSX def2-TZVP def2/J TightSCF  
```
- `TightSCF` for tight convergence

```
%scf
  MaxIter 150
end
```
- Maximum number of SCF cycles

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

# 7. Special cases
## 7.1 UHF
```
----------------------
UHF SPIN CONTAMINATION
----------------------

Expectation value of <S**2>     :     2.005700
Ideal value S*(S+1) for S=1.0   :     2.000000
Deviation                       :     0.005700
```
- If the expectation value of the (written as <S**2>) operator differs significantly from the ideal value, it might be that your system could only be treated with a multi-reference calculation such as CASSCF.
## 7.2 T1 diagnostic
```
----------------------
COUPLED CLUSTER ENERGY
----------------------

E(0)                                       ...    -76.055469404
E(CORR)(strong-pairs)                      ...     -0.267934936
E(CORR)(weak-pairs)                        ...     -0.000104148
E(CORR)(corrected)                         ...     -0.268039083
E(TOT)                                     ...    -76.323508487
Singles Norm <S|S>**1/2                    ...      0.018648176
T1 diagnostic                              ...      0.006593126
```
- Please always check the T1 diagnostic value printed. A rule of thumb says, that for a value of the diagnostic of larger than 0.02 the results are not to be trusted and the HF reference might be poor.

# 8. Techniques

## 8.1 Resolution of identity
```
!HF DEF2-SVP DEF2/J RIJDX
```
- RI with `RIJDX`
```
!HF DEF2-SVP DEF2/J RIJCOSX
```
- RI with `RIJCOSX`
```
!HF DEF2-SVP AUTOAUX RIJCOSX
```
- RI with `RIJCOSX` with `AUTOAUX`

## 8.2 Dispersion corrections
-DFT is known to perform poorly with intermolecular or weak interactions. In general it is advisable to use the D3 [Goerigk2011] or the charge-dependent D4 [Grimme2017] corrections using `!B3LYP DEF2-SVP OPT D3` or `!B3LYP DEF2-SVP OPT D4`.

## 8.3 CBS Extrapolation
- The `EXTRAPOLATE(3)` keyword here means that three calculations using the basis set from the family cc-pVxZ (where x is D, T and then Q) will be done and the CBS results will be extrapolated from that.
```
!DLPNO-CCSD(T) EXTRAPOLATE(3) cc-pVQZ/C
```
- The /C basis is not automatically chosen, so it is best to use the one corresponding to the largest basis.
```
!DLPNO-CCSD(T) EXTRAPOLATE(3) AUTOAUX
```
- AUTOAUX for /C basis

### 8.3.1 2-point extrapolation
```
Extrapolate(X/Y,basis)
```
- `X/Y` are successive cardinal numbers and `basis = cc, aug-cc, cc-core, ano, saug-ano, aug-ano, def2`
- `Extrapolate(2/3,cc)` or `Extrapolate(3/4,cc)`


### 8.3.2 n-point extrapolation
```
Extrapolate(n,basis)
```
- Calculate the first n-energies for members of the basis set family basis, e.g. Extrapolate(3,cc) is for 3-point extrapolation with cc-pVDZ, cc-pVTZ and cc-pVQZ.
  
### 8.3.3 ExtrapolateEP2 with MP2
- For the ExtrapolateEP2, and ExtrapolateEP3 keywords the default cheap method is the DLPNO-CCSD(T) with the NormalPNO thresholds.
```
! ExtrapolateEP2(2/3,ANO,MP2) TightSCF Conv Bohrs
```
- Extrpolate MP2
```
Alpha     :  5.410 (SCF Extrapolation)
Beta      :  2.430 (correlation extrapolation)
SCF energy with basis ano-pVDZ:                   -76.059178452
SCF energy with basis ano-pVTZ:                   -76.064774379
Extrapolated CBS SCF energy :                     -76.065995735 (-0.001221356)
MP2 energy with basis ano-pVDZ:                    -0.219202871
MP2 energy with basis ano-pVTZ:                    -0.267058634
Extrapolated CBS correlation energy :              -0.295568604 (-0.028509970)
CCSD(T) correlation energy with basis ano-pVDZ:    -0.229478341
CCSD(T) - MP2 energy with basis ano-pVDZ:          -0.010275470
Estimated CBS total energy :                      -76.371839809
```
### 8.3.4 ExtrapolateEP2 with MDCI
- For the ExtrapolateEP2, and ExtrapolateEP3 keywords the default cheap method is the DLPNO-CCSD(T) with the NormalPNO thresholds.
```
! ExtrapolateEP2(2/3,cc,DLPNO-CCSD(T)) TightSCF Conv Bohrs
```
- Extrapolate MDCI
```
Alpha     :  4.420 (SCF Extrapolation)
Beta      :  2.460 (correlation extrapolation)
SCF energy with basis cc-pVDZ:                      -76.026430944
SCF energy with basis cc-pVTZ:                      -76.056728252
Extrapolated CBS SCF energy :                       -76.066581429 (-0.009853177)
MDCI energy with basis cc-pVDZ:                      -0.214429497
MDCI energy with basis cc-pVTZ:                      -0.275299699
Extrapolated CBS correlation energy :                -0.310868368 (-0.035568670)
CCSD(T) correlation energy with basis cc-pVDZ:       -0.214548320
CCSD(T) - MDCI energy with basis cc-pVDZ:            -0.000118824
Estimated CBS total energy :                        -76.377568621
```

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
