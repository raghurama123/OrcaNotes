# Orca usage notes
# Basis Input

```
!HF DEF2-SVP
* xyz 0 1
O         -3.56626        1.77639        0.00000
H         -2.59626        1.77639        0.00000
H         -3.88959        1.36040       -0.81444
*
```
# Read geometry from a file

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

# Geometry Optimization

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
- DLPNO-MP2
