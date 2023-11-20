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
!DLPNO-CCSD(T) EXTRAPOLATE(3) CC-PVQZ/C
```
- The /C basis is not automatically chosen, so it is best to use the one corresponding to the largest basis.
```
!DLPNO-CCSD(T) EXTRAPOLATE(3) AUTOAUX
```
- AUTOAUX for /C basis

### 8.3.1 2-point extrapolation
```
EXTRAPOLATE(X/Y,basis)
```
- `X/Y` are successive cardinal numbers and `basis = CC, AUG-CC, CC-CORE, ANO, SAUG-ANO, AUG-ANO, DEF2`
- `EXTRAPOLATE(2/3,CC)` or `EXTRAPOLATE(3/4,CC)`


### 8.3.2 n-point extrapolation
```
EXTRAPOLATE(n,basis)
```
- Calculate the first n-energies for members of the basis set family basis, e.g. EXTRAPOLATE(3,CC) is for 3-point extrapolation with cc-pVDZ, cc-pVTZ and cc-pVQZ.
  
### 8.3.3 ExtrapolateEP2 with MP2
- For the EXTRAPOLATEEP2, and EXTRAPOLATEEP3 keywords the default cheap method is the DLPNO-CCSD(T) with the `NORMALPNO` thresholds.
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
! EXTRAPOLATEEP2(2/3,CC,DLPNO-CCSD(T)) TIGHTSCF CONV BOHRS
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
