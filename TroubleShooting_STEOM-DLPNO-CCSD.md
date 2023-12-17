# 14.1 Troubleshooting STEOM-DLPNO-CCSD

## 14.1.1 Excerpts from the Manual

- `TIGHTSCF` is a must go for any CCSD calculation.
- We will recommend using `TIGHTPNO` for all molecules as it is not a lot more expensive and helps to achieve
a better convergence.
- The `OTHRESH`, `VTHRESH` and `TCutPNOSingles` keywords help with converging the calculations, increasing
the percentage active of each root.
  - In contrary to standard STEOM-CCSD, we would acknowledge that the roots converge when the percentage active character is at least 96 %. Of course, you have to check that the amplitude and orbitals associated with the excitation are correct (and what you expect).
  - Tightening the 3 keywords mentioned will increase this percentage active character. The most important one is the `TCutPNOSingles` one. Be careful the computational cost increases exponentially when tightened. In more case `1e-12` or `5e-12` should be enough.
  - For `OTHRESH` and `VTHRESH` you should not go below `1e-3`, as the benefits are not so obvious. Another trick to achieve a better convergence is to play with the number of roots. It is often not necessary to compute a lot of roots if you are only interested in the first 3 for example. If some high energy roots have some low percentage active character, removing them can help for the convergence of
other roots.

## 14.1.2 Convergence options
- Here are the possible values and their definition
```
%MDCI
  TCUTPAIRS       1e-4         # cut-off  for the  pair truncation
  TCUTPNO         3.33e-7      # cut-off  for the  PNO truncation
  TCUTDO          1e-2         # cut-off  for the  DLPNO domain construction
  TCUTMKN         1e-3         # cut-off  for the  local fit
  TCUTPNOSINGLES -1            # -1= use 0.03*TCutPNO
  OThresh         0.001        # Cut-off occupation of CIS natural orbitals in IP calculation
  VThresh         0.001        # Cut-off occupation of CIS natural orbitals in EA calculation
  IPSThrs         80           #  The percentage singles threshold for the IP calculation
  EASThrs         80           #  The percentage singles threshold for the EA calculation
END

```
- Here are all the options, but we usually will not explicitly change these in the input file but will choose one of the options given above.
- `TightPNO` triggers the full iterative (DLPNO-MP2) treatment in the MP2 guess, whereas the other options use a semicanonical MP2 calculation.

| Parameter | LoosePNO | NormalPNO | TightPNO | 
|---|---|---|---|
| TCutPairs      | 1E-3   | 1E-4  | 1E-5   |
| TCutDO   | 2E-2   | 1E-2  | 5E-3   |
| TCutPNO   | 1E-6   | 3.33E-7  | 1E-7   | 
| TCutMKN    | 1E-3   | 1E-3  | 1E-3   |
| MP2 pair treatment      | semicanonical   | semicanonical  | full iterative   |
|TCutPNOSingles | 3E-8 | 1E-8 | 3E-9 |

## 14.1.3 Case: Z-diazo derivative from the manual [https://www.orcasoftware.de/tutorials_orca/spec/UVVis.html](https://www.orcasoftware.de/tutorials_orca/spec/UVVis.html)

```
!STEOM-DLPNO-CCSD DEF2-TZVP DEF2-TZVP/C RIJCOSX TightSCF CPCM(HEXANE)

%MDCI
   NROOTS  10
   DOSOLV  TRUE
   MAXITER 500
END

* XYZFILE 0 1 Z_azo_opt.xyz

%pal nproc 16
end

```

- B3LYP D4 Def2TZVP
```
28
Coordinates from ORCA-job Z_azo_opt
  N   -0.63743882637434     -0.79668673601102      1.83215036994703
  N   0.59518168829060     -0.90834343089653      1.80248635006688
  C   -2.90717393453564      0.14454097832725     -1.58531306566676
  C   -2.87983888975854     -1.14517514791771     -1.06893263617567
  C   -2.11991529512837     -1.41225321505075      0.05920370369417
  C   -1.36285778151479     -0.40395118652168      0.64962561082718
  C   -1.39231704513710      0.90783363329687      0.16384818854752
  C   -2.17710708280823      1.14906354926722     -0.96541774507155
  C   -0.66206054223081      2.05829799407404      0.81225563029536
  C   0.84698632609233      1.84690984382174      1.12478664316725
  C   1.50490715856188      0.78735549918981      0.28830393383847
  C   2.29393122337135      1.08778067722381     -0.81877394682909
  C   2.88206368718192      0.08298656582408     -1.57796563128321
  C   2.70343253490175     -1.25003954751574     -1.22384774568744
  C   1.93975856723153     -1.57374854906724     -0.11047591540394
  C   1.32642098354228     -0.56015079695017      0.61477749589269
  H   -3.49948703454962      0.37031392160539     -2.46277023257439
  H   -3.44927643588200     -1.93826491327290     -1.53627109708714
  H   -2.09379012259540     -2.40528294530250      0.48951445061872
  H   -2.20731871876996      2.15509475173048     -1.36692910064281
  H   -1.16987880430591      2.32758505668668      1.74339793542879
  H   -0.76512158481951      2.91770414682640      0.14912678585690
  H   0.96193765274915      1.58679935968746      2.17811033513225
  H   1.36413674421323      2.79581360087073      0.97972257689835
  H   2.44688461704361      2.12668688836562     -1.08711350219598
  H   3.48817331872739      0.34024210569775     -2.43722135326218
  H   3.16604010372158     -2.03673781103272     -1.80597032766688
  H   1.80513849278162     -2.60373329295635      0.19411628933549

```

```
IROOT=  1:  0.129149 au     3.514 eV   28345.0 cm**-1
  Amplitude    Excitation
  -0.527196    50 ->  55
  -0.534252    50 ->  59
  -0.139044    50 ->  61
  -0.127235    53 ->  55
  -0.143267    53 ->  59
  -0.420985    54 ->  55
  -0.374939    54 ->  59
  Ground state amplitude:  0.078950

Percentage Active Character     97.15

Warning:: the state may have not converged with respect to active space 
-------------------- Handle with Care -------------------- 
```

- wB97XD def2TZVP

```
28
Coordinates from ORCA-job Z_wB97XD3_opt
  N   -0.63605909679261     -0.77955053967214      1.84322373678372
  N   0.59075495331295     -0.88914274316197      1.81591188047580
  C   -2.87504711350362      0.13977597290284     -1.59014023427344
  C   -2.83800315753550     -1.14873962073396     -1.08121388130014
  C   -2.08738465386011     -1.41217845479938      0.05082507626804
  C   -1.35510210595736     -0.39839659496403      0.65315442579066
  C   -1.38976098995388      0.91085391204874      0.17242574008319
  C   -2.16290235965338      1.14796034340702     -0.96150315365689
  C   -0.66069481980864      2.06084588573111      0.82427895342598
  C   0.84500402804729      1.85083731715587      1.12965476849853
  C   1.49985339812499      0.78896187268609      0.29223002204076
  C   2.27679846061365      1.08244792069693     -0.82142289652149
  C   2.84930413385846      0.07387976724523     -1.58253473242993
  C   2.66321068473346     -1.25399165671149     -1.22753326289718
  C   1.90860541118401     -1.57089524384942     -0.10919799345070
  C   1.31728299540078     -0.55322087115049      0.62108794844861
  H   -3.46114989768816      0.36286837697494     -2.47316719398799
  H   -3.39171830293546     -1.94708875202006     -1.55968206547483
  H   -2.05155237466265     -2.40748453682412      0.47749582136881
  H   -2.19692399520887      2.15489188943682     -1.36273408606246
  H   -1.16960567805330      2.32574158732178      1.75529984252191
  H   -0.76732920952778      2.92140282428543      0.16280853434376
  H   0.96788134441178      1.59141893115998      2.18257477710764
  H   1.36302823149497      2.79897233089521      0.98246901737458
  H   2.43349214764336      2.12056964298168     -1.09389665875639
  H   3.44909636667105      0.32566052183029     -2.44864100382647
  H   3.11487469073301     -2.04522996908008     -1.81315650936011
  H   1.76545790891159     -2.60052911379281      0.19580712746606
```

```

IROOT=  1:  0.117369 au     3.194 eV   25759.6 cm**-1
  Amplitude    Excitation
   0.721858    50 ->  55
   0.320676    50 ->  59
   0.172064    53 ->  55
   0.499435    54 ->  55
   0.212655    54 ->  59
  Ground state amplitude:  0.008246

Percentage Active Character     97.23

Warning:: the state may have not converged with respect to active space 
-------------------- Handle with Care -------------------- 
```

## 14.1.4 Solution
- The calculations converged with `TIGHTPNO`

```
B3LYP geom
IROOT=  1:  0.108872 au     2.963 eV   23894.6 cm**-1

wB97X-D3 geom
IROOT=  1:  0.111334 au     3.030 eV   24434.9 cm**-1
``` 


