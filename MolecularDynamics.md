# 11. Molecular Dynamics

- In contrast to general ORCA input, the MD input is not based on keywords, but on commands, which are executed consecutively on a line-by-line basis starting at the top (like, e. g., in a shell script). This means that identical commands with different arguments may be given, coming into effect when the interpreter reaches the corresponding line. This enables to perform multiple simulations (e. g., pre-equilibration and production run) within a single input file:

```
%MD
  TIMESTEP 1.0_fs
  RUN      200
  TIMESTEP 2.0_fs
  RUN      500
END
```

## 11.1 Water dimer trajectory
```
! MD BLYP D3 DEF2-SVP

%MD
  INITVEL              300_K
  THERMOSTAT BERENDSEN 300_K TIMECON 10.0_fs
  TIMESTEP             0.5_fs
  RUN                  2000
  DUMP POSITION STRIDE 1 FILENAME "trajectory.xyz"
END

%MAXCORE 4000

%PAL
  NPROCS 24
END

* XYZ 0 1
O    -2.03740    -1.21799    -0.08342
H    -1.06493    -1.04408    -0.02285
H    -2.37327    -1.07034     0.83692
O    -1.65042     1.84243     0.07893
H    -0.72656     1.49786    -0.01029
H    -2.07086     1.65422    -0.79801
*
```

## `TIMECON`
- The `Timecon` modifier sets the coupling strength of the thermostat (large time constants correspond to weak coupling). The default value is 10 fs, which is a relatively strong coupling. For a production run, 100 fs would be appropriate.

## `TIMESTEP`
```
%MD
  TIMESTEP  1.0_fs
  TIMESTEP 41.3_au # identical, 1 au = 0.02419 fs
  TIMESTEP  1.0    # identical, as default time unit in MD module is fs
END
```

## `RESTART`
- If `basename.mdrestart` exists, restart using
```
%MD
  ...
  RESTART IFEXISTS
  RUN     100
END
```
