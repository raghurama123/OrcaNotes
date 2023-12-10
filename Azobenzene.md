# 13. UV/Visible Spectrum of Z/E Isomers of Azobenzene

The following is based on [https://www.orcasoftware.de/tutorials_orca/spec/UVVis.html](https://www.orcasoftware.de/tutorials_orca/spec/UVVis.html).   

## 13.1 Initial geometries

- Initial geometries created with Avogadro are as follows
- cis-isomer
```
28
z-azobenzene
N         -2.63769       -1.11104        1.70607
N         -1.46758       -0.68047        1.84509
C         -3.54394       -0.69969        0.70370
C         -0.72646        0.17669        0.96391
C         -1.04152        1.53323        0.58133
C         -0.11571        2.22755       -0.22754
C          1.06595        1.63475       -0.66278
C          1.36677        0.33345       -0.28962
C          0.48655       -0.37792        0.51989
H         -0.31139        3.25003       -0.53048
H          1.75427        2.19155       -1.28568
H          2.29053       -0.12439       -0.61947
H          0.75499       -1.38660        0.81121
C         -2.25419        2.37413        0.96403
C         -3.40515        1.63688        1.61002
H         -2.66086        2.85044        0.04265
H         -1.91375        3.19402        1.63309
C         -4.82715        1.03770       -0.39280
C         -3.93981        0.63797        0.62148
C         -5.33318        0.09721       -1.29484
C         -4.95752       -1.24443       -1.18932
C         -4.06615       -1.64350       -0.18943
H         -4.21782        2.33853        1.89867
H         -3.05408        1.17601        2.55615
H         -3.77273       -2.68324       -0.11647
H         -6.02105        0.40709       -2.07087
H         -5.35377       -1.97373       -1.88396
H         -5.13339        2.07310       -0.47650
```
- trans-isomer
```
28
e-azobenzene
N         -1.52660        0.98829        0.39578
N         -0.78460        1.14002       -0.58471
C         -2.89819        1.07178        0.17620
C          0.26065        2.04993       -0.45833
C         -0.05528        3.42065       -0.54513
C          0.99385        4.34942       -0.38545
C          2.30382        3.91750       -0.14935
C          2.59194        2.55304       -0.07407
C          1.56996        1.61555       -0.22897
H          0.80490        5.41360       -0.45075
H          3.09803        4.64319       -0.03015
H          3.60672        2.22296        0.10685
H          1.79244        0.55796       -0.16262
C         -1.47638        3.93043       -0.85705
C         -2.62524        3.64805        0.15832
H         -1.79929        3.61425       -1.87181
H         -1.39473        5.03928       -0.89683
C         -4.83857        2.44714       -0.24068
C         -3.45460        2.35647        0.01466
C         -5.62814        1.29515       -0.32899
C         -5.05359        0.03366       -0.15871
C         -3.68613       -0.08065        0.09489
H         -3.34567        4.48387        0.01622
H         -2.23461        3.75782        1.19241
H         -3.23967       -1.05927        0.21896
H         -6.68921        1.38191       -0.52444
H         -5.66800       -0.85485       -0.22595
H         -5.31585        3.41107       -0.36509
```

## 13.2 Geometry optimization

- Here is the input file for Z-isomer. Change accordingly for the E-isomer.

```
!WB97X-D3 RIJCOSX DEF2-TZVP DEF2/J TIGHTSCF OPT FREQ CPCM(HEXANE)

* XYZFILE 0 1 Z_azobenzene.xyz

%MAXCORE 5000

%PAL
  NPROCS 24
END

%GEOM
  CALC_HESS TRUE
  RECALC_HESS 5
  MAXITER 50
END
```

## 13.3 TDDFT

- Here is the input file for Z-isomer. Change accordingly for the E-isomer.

```
!WB97X-D3 RIJCOSX DEF2-TZVP DEF2/J TIGHTSCF CPCM(HEXANE)

* XYZFILE 0 1 Z_opt.xyz

%MAXCORE 5000

%PAL
  NPROCS 24
END

%TDDFT
 NROOTS       20
 IROOT        1
 TDA          FALSE
 TRIPLETS     FALSE
END
```
