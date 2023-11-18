# Orca usage notes

# Input control
## Basis Input

```
!HF DEF2-SVP
* xyz 0 1
O         -3.56626        1.77639        0.00000
H         -2.59626        1.77639        0.00000
H         -3.88959        1.36040       -0.81444
*
```
## Read geometry from a file

* To load the geometry from a file, try
```
!HF DEF2-SVP XYZFILE
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
## Store final geometry in a file

```
!HF DEF2-SVP XYZFILE Opt
%base "geom_final"
* xyz 0 1 geom_init.xyz
```
- The final geometry will be stored in the file `geom_final.xyz`

# Memory and cores
```
%MaxCore 4000

%pal nprocs 8
end
```
- 4GB per core and 8 cores for this calculation.

## Optimal memory for helios

- `%MaxCore 4000` qa, qb
- `%MaxCore 5000` qd
- `%MaxCore 14000` q
- `%MaxCore 16000` qc


# Methods
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
  
# Single Point Energy

## SCF Convergence

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

# Geometry Optimization
```
!wB97X-D3 RIJCOSX def2-TZVP def2/J TightSCF TightOpt 
```
- `TightSCF` and `TightOpt` for tight convergence criteria for SCF convergence and geometry convergence

## Calculate Hessian
```
%geom
  Calc_Hess true
  Recalc_Hess 5
  MaxIter 50
end
```

## Numerical Gradient
```
!DLPNO-CCSD(T) cc-pVTZ cc-pVTZ/C OPT NUMGRAD
```

# Vibrational Frequencies

# Special cases
## UHF
```
----------------------
UHF SPIN CONTAMINATION
----------------------

Expectation value of <S**2>     :     2.005700
Ideal value S*(S+1) for S=1.0   :     2.000000
Deviation                       :     0.005700
```
- If the expectation value of the (written as <S**2>) operator differs significantly from the ideal value, it might be that your system could only be treated with a multi-reference calculation such as CASSCF.
## T1 diagnostic
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

# Techniques

## Resolution of identity
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

# Check Convergence
## Energy
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

## Geometry
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
- DLPNO-MP2
