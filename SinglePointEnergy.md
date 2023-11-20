# 4. Single Point Energy

## 4.1 SCF convergence

```
!WB97X-D3 RIJCOSX DEF2-TZVP DEF2/J TIGHTSCF
```
- `TIGHTSCF` for tight convergence

```
%SCF
  MAXITER 150
END
```
- Maximum number of SCF cycles
- Alternatively, remove `TIGHTSCF` from the title line and use
```
%SCF
  MAXITER 150
  TIGHT
END
```

- It is probably best to define the SCF convergence option on the title line.
- Possible values are `LOOSESCF`, `SLOPPYSCF`, `NORMALSCF` (this is the default), `STRONGSCF`, `TIGHTSCF`, `VERYTIGHTSCF`, `EXTREMESCF`


## 4.2 Convergence options
- Here are the possible values and their definition
```
%SCF
  CONVERGENCE # The default convergence is between medium and strong 
  SLOPPY      # very weak convergence 
  LOOSE       # still weak convergence
  MEDIUM      # intermediate accuracy
  STRONG      # stronger 
  TIGHT       # still stronger
  VERYTIGHT   # even stronger
  EXTREME     # close to the numerical zero of the computer in double-precision arithmetic
END
```
- Here are all the options but we normally will not explicitly change these in the input file but will choose one of the options given above.

| Parameter | Sloppy | Loose | Medium | Normal | Strong | Tight | VeryTight | Extreme |
|---|---|---|---|---|---|---|---|---|
| TolE      | 3E-5   | 1E-5  | 1E-6   | 1E-6   | 3E-7   | 1E-8  | 1E-9      | 1E-14   |
| TolMaxP   | 1E-4   | 1E-3  | 1E-5   | 1E-5   | 3E-6   | 1E-7  | 1E-8      | 1E-14   |
| TolRMSP   | 1E-5   | 1E-4  | 1E-6   | 1E-6   | 1E-7   | 5E-9  | 1E-9      | 1E-14   | 
| TolErr    | 1E-4   | 5E-4  | 1E-5   | 1E-6   | 3E-6   | 5E-7  | 1E-8      | 1E-14   |
| TolG      | 3E-4   | 1E-4  | 5E-5   | 5E-5   | 2E-5   | 1E-5  | 2E-6      | 1E-09   |
| TolX      | 3E-4   | 1E-4  | 5E-5   | 5E-5   | 2E-5   | 1E-5  | 2E-6      | 1E-09   |

- `TolE` is energy change between two cycles, `Last Energy change`
- `TolRMSP` is RMS density change, `Last MAX-Density change`
- `TolMaxP` is maximum density change, `Last RMS-Density change`
- `TolErr` is DIIS error convergence, ``
- `TolG` is orbital gradient convergence, `Last RMS-Density change`
- `TolX` is orbital rotation angle convergence, `Last RMS-Density change`
