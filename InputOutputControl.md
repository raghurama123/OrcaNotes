# 1. Input/Output control

## 1.1 Basic Input

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
* XYZFILE 0 1 geom_init.xyz
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
* XYZFILE 0 1 geom_init.xyz
```
- If the input file is test.com, the final geometry will be stored in the file `test.xyz`

## 1.4 Change basename
```
!HF DEF2-SVP Opt XYZFILE
%base "HF_SVP"
* XYZFILE 0 1 geom_init.xyz
```
- If the input file is test.com, the final geometry will be stored in the file `HF_SVP.xyz`. All the files, expect the output file will have the basename "HF_SVP"
