# 13. UV/Visible Spectrum of Z/E Isomers of Azobenzene

The following is based on [https://www.orcasoftware.de/tutorials_orca/spec/UVVis.html](https://www.orcasoftware.de/tutorials_orca/spec/UVVis.html).   

## 13.1 Initial geometries

- Initial geometries created with Avogadro are as follows
- cis-isomer
```
28
Z
N -0.618886 -0.883112 1.731709
N 0.609782 -1.018485 1.682439
C -3.149784 0.161082 -1.476635
C -3.126067 -1.121614 -0.940862
C -2.268677 -1.401151 0.108970
C -1.398180 -0.426127 0.604236
C -1.423557 0.881062 0.096547
C -2.315554 1.135813 -0.952342
C -0.617308 2.049069 0.627623
C 0.823679 1.776817 1.115925
C 1.562257 0.759864 0.289180
C 2.438948 1.120736 -0.733271
C 3.104755 0.160800 -1.485427
C 2.920865 -1.189857 -1.205541
C 2.078455 -1.573467 -0.171975
C 1.380794 -0.604192 0.545112
H -3.818097 0.403014 -2.292443
H -3.776124 -1.894502 -1.329033
H -2.252341 -2.382436 0.564684
H -2.346616 2.136199 -1.367177
H -1.170931 2.520332 1.446423
H -0.576530 2.792221 -0.170484
H 0.800661 1.447635 2.155139
H 1.367038 2.722747 1.104189
H 2.601046 2.172258 -0.939281
H 3.776150 0.465143 -2.277520
H 3.445224 -1.942265 -1.779820
H 1.950409 -2.616943 0.084059
```
- trans-isomer
```
28
E
N -0.367763 -0.503565 -1.012256
N 0.367727 0.501058 -1.014376
C 1.699781 0.196441 -0.639281
C -1.699892 -0.197832 -0.638447
C -1.806595 0.262669 0.689143
C -3.094602 0.449760 1.187893
C -4.220566 0.202705 0.407827
C -4.081481 -0.272253 -0.891820
C -2.813034 -0.496315 -1.411644
C 2.813048 0.496483 -1.411925
C 4.081485 0.274404 -0.891468
C 4.220598 -0.200188 0.408333
C 3.094632 -0.448481 1.187906
C 1.806541 -0.263003 0.688663
C -0.587112 0.516610 1.579363
C 0.587164 -0.518405 1.578669
H -3.218763 0.794292 2.208638
H -5.207355 0.363877 0.823612
H -4.957017 -0.476936 -1.495020
H -2.678112 -0.883915 -2.413542
H 2.678190 0.883116 -2.414204
H 4.956913 0.479713 -1.494616
H 5.207413 -0.359883 0.824621
H 3.218988 -0.792080 2.208940
H -0.184377 1.511396 1.372571
H -0.964360 0.560324 2.603343
H 0.964632 -0.562884 2.602561
H 0.184731 -1.513104 1.371002
```

## 13.2 Geometry optimization

- Here is the input file for E-isomer. Change accordingly for the Z-isomer.

```
!WB97X-D3 RIJCOSX DEF2-TZVP AUTOAUX TIGHTSCF OPT FREQ CPCM(HEXANE)

* XYZFILE 0 1 E_azobenzene.xyz

%MAXCORE 5000

%PAL
  NPROCS 18
END

%GEOM
  CONVERGENCE TIGHT
  CALC_HESS TRUE
  RECALC_HESS 5
  MAXITER 50
END
```

## 13.3 TDDFT

- Here is the input file for E-isomer. Change accordingly for the Z-isomer.

```
!WB97X-D3 RIJCOSX DEF2-TZVP AUTOAUX TIGHTSCF CPCM(HEXANE)

* XYZFILE 0 1 E_opt.xyz

%MAXCORE 5000

%PAL
  NPROCS 18480
END

%TDDFT
 NROOTS       20
 TDA          FALSE
 TRIPLETS     FALSE
END
```

## 13.4 STEOM-DLPNO-CCSD

- Here is the input file for E-isomer. Change accordingly for the Z-isomer.

```
!STEOM-DLPNO-CCSD DEF2-TZVP AUTOAUX RIJCOSX CPCM(HEXANE) TIGHTSCF

* XYZFILE 0 1 E_opt.xyz

%MAXCORE 5000

%PAL
  NPROCS 18
END

%MDCI
   NROOTS  5
   DOSOLV  TRUE
   MAXITER 500
END
```

## 13.5 Results

- Wavelength of absorbance for E and Z isomers.
- Geometry optimized using reported geometries at the level `wB97X-D3/def2TZVP`
- `def2TZVP RIJCOSX TIGHTSCF CPCM(HEXANE) AUTOAUX` unless mentioned in all calculations
- By default, `STEOM-DLPNO-CCSD` uses `NormalPNO`


| Method | E | Z | Remarks |
|---|---|---|---|
|PBE0               |504   |413||
|B3LYP              |505   |418 |(507 and 417 in Orca's tutorial page)|
|CAM-B3LYP          |485   |407||
|wB97X-D3           |480   |402||
|                   |463   |388 |TDA True|
|                   |      | 405 |B3LYP D4 geom, 3.059 eV|
|                   |      |402 |wB97X-D3 geom, 3.084 eV|
|wB2PLYP            |474   |396||
|STEOM-DLPNO-CCSD   |509   |392 |shift 117 nm|
|STEOM-DLPNO-CCSD   |505   |411 |TightPNO (shift of 94 nm)|
|STEOM-DLPNO-CCSD   |509   |392 |DEF2-TZVP/C instead of AUTOAUX|
|                  |2.46   |3.18 eV |shift 0.72 eV|
|                   |      |421 |TightPNO, B3LYP D4 geom, 2.963 eV|
|                   |      |412 |TightPNO, wB97X-D3 geom), 3.030 eV|
|                   |      |424 |TightPNO, TCutPNOSingles 1E-12, B3LYP D4 geom, 2.944 eV|
|                   |      |429 |TightPNO, TCutPNOSingles 1E-12, wB97X-D3 geom, 2.907 eV|
|                   |      |431 |TightPNO, TCutPNOSingles 1E-12, TCutMKN 1E-4, B3LYP geom, 2.897 eV|
|                   |      |426 |TightPNO, TCutPNOSingles 1E-12, TCutMKN 1E-4, wB97X-D3 geom, 2.931 eV|
|RI-ADC2/VDZ/Qchem  |455   |372||
|                  |2.73  |3.34  eV||
|RI-ADC2/VTZ/Qchem  |    |||
|Exp.               |490   |404 |shift 86 nm|
|                  |2.53   |3.07 eV |shift 0.54 eV   |

## 13.6 Effect of `AUTOAUX` in STEOM-DLPNO-CCSD
- Let's do this experiment with geometries at the level `wB97X-D3/def2TZVP`
- `DEF2TZVP RIJCOSX TIGHTSCF CPCM(HEXANE)` unless specified otherwise  
  
| Method | E | Z | Remarks |
|---|---|---|---|
|STEOM-DLPNO-CCSD   |509   |392 |LoosePNO, DEF2-TZVP/C|
|STEOM-DLPNO-CCSD   |505   |411 |LoosePNO, AUTOAUX|
|STEOM-DLPNO-CCSD   |509   |392 |NormalPNO, DEF2-TZVP/C|
|STEOM-DLPNO-CCSD   |505   |411 |NormalPNO, AUTOAUX|
|STEOM-DLPNO-CCSD   |509   |392 |TightPNO, DEF2-TZVP/C|
|STEOM-DLPNO-CCSD   |505   |411 |TightPNO, AUTOAUX|
|Exp.               |490   |404 |shift 86 nm|

