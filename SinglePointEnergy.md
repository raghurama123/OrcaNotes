# 4. Single Point Energy

## 4.1 SCF convergence

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
- Alternatively, remove `TightSCF` from the title line and use
```
%scf
  MaxIter 150
  Tight
end
```

## 4.2 Convergence options
- Here are the possible values and their definition
```
%scf
  Convergence # The default convergence is between medium and strong 
  Sloppy      # very weak convergence 
  Loose       # still weak convergence
  Medium      # intermediate accuracy
  Strong      # stronger 
  Tight       # still stronger
  VeryTight   # even stronger
  Extreme     # close to the numerical zero of the computer in double-precision arithmetic
end
```
- Here are all the options but we normally will not explicitly change these in the input file but will choose one of the options given above.

| Parameter | Sloppy | Loose | Medium | Strong | Tight | VeryTight | Extreme |
|---|---|---|---|---|---|---|---|
| TolE      | 3E-5   | 1E-5  | 1E-6   | 3E-7   | 1E-8  | 1E-9      | 1E-14   |
| TolMaxP   | 1E-4   | 1E-3  | 1E-5   | 3E-6   | 1E-7  | 1E-8      | 1E-14   |
| TolRMSP   | 1E-5   | 1E-4  | 1E-6   | 1E-7   | 5E-9  | 1E-9      | 1E-14   | 
| TolErr    | 1E-4   | 5E-4  | 1E-5   | 3E-6   | 5E-7  | 1E-8      | 1E-14   |
| TolG      | 3E-4   | 1E-4  | 5E-5   | 2E-5   | 1E-5  | 2E-6      | 1E-09   |
| TolX      | 3E-4   | 1E-4  | 5E-5   | 2E-5   | 1E-5  | 2E-6      | 1E-09   |

- `TolE` is energy change between two cycles, `Last Energy change`
- `TolRMSP` is RMS density change, `Last MAX-Density change`
- `TolMaxP` is maximum density change, `Last RMS-Density change`
- `TolErr` is DIIS error convergence, ``
- `TolG` is orbital gradient convergence, `Last RMS-Density change`
- `TolX` is orbital rotation angle convergence, `Last RMS-Density change`
