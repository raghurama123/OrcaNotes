## 15.2 NBO analysis of the C<sub>6</sub>H<sub>6</sub>···HF complex

The benzene–HF complex provides a simple example of an X–H···$\pi$ hydrogen bond. Benzene acts primarily as an electron donor, while the antibonding orbital of HF acts as the acceptor.

The dominant donor–acceptor interaction is

$$
\pi_{\mathrm{C_6H_6}}
\rightarrow
\sigma^\ast_{\mathrm{H-F}}.
$$

---

### 15.2.1 Optimized geometry

The optimized geometry is stored in `opt.xyz`.

```text
14
Coordinates from ORCA-job opt E -332.547916999280
  F          -0.36591673791697     -0.56492759064254      3.17367925797555
  H          -0.38497593656210     -0.58762002178632      2.23801713529204
  C           0.07511437888785      1.48251694509552     -0.29936586387641
  C           1.27551341774749      0.76375067709013     -0.31193773680713
  C           1.26463875559622     -0.62166239553779     -0.13010871750794
  C           0.05026872435457     -1.29234169045155      0.06167181148190
  C          -1.15230355599585     -0.57268186155157      0.07377450660508
  C          -1.13788794410909      0.81652243849082     -0.10551088695551
  H           0.08640216117589      2.56007072898033     -0.43528387864471
  H           2.21776693558452      1.28404811141667     -0.45763158392622
  H           2.19656193289675     -1.17929541386890     -0.13417344776620
  H           0.03970002516255     -2.36997547393793      0.19902345030997
  H          -2.09522841241036     -1.09266095370666      0.21849452528354
  H          -2.06965374441146      1.37425650040979     -0.09064857146397
```

The H–F bond length is approximately

$$
r_{\mathrm{H-F}}=0.936\ \text{Å}.
$$

The hydrogen atom of HF lies approximately $2.20$ Å above the benzene plane.

The position of HF is not exactly above the center of the ring. The hydrogen is directed toward the region of the C6–C7 bond, with an H-to-C6–C7 bond-midpoint distance of approximately $2.20$ Å.

The H–F bond is nearly perpendicular to the benzene plane. The angle between the H–F axis and the normal to the ring plane is approximately $7^\circ$.

Thus, the optimized structure is an off-center H–F···$\pi$ complex in which the positive end of HF points toward one part of the benzene $\pi$ cloud.

---

### 15.2.2 ORCA input for the NBO calculation

The NBO input is the same as that used for H<sub>2</sub>.

```text
! B3LYP 6-31+G(d,p) def2/J RIJCOSX TightSCF NBO

* xyzfile 0 1 opt.xyz

%base "nbo"

%MaxCore 8000

%scf
  MaxIter 150
end

%pal
  nprocs 2
end
```

The geometry is read from `opt.xyz`, and the `NBO` keyword sends the converged wavefunction to NBO 7.0 for analysis.

---

### 15.2.3 Molecular units identified by NBO

NBO separates the system into two molecular units:

```text
Molecular unit 1  (HF)
Molecular unit 2  (C6H6)
```

This means that NBO retains the conventional Lewis structures of HF and benzene.

In particular, NBO does not identify a new covalent bond between the HF hydrogen and any carbon atom of benzene.

The system is therefore described as a noncovalent

$$
\ce{C6H6\cdots H-F}
$$

complex rather than protonated benzene.

---

### 15.2.4 Natural charges

The natural charges on the atoms of HF are

```text
F  1   -0.59850
H  2    0.58559
```

HF therefore remains strongly polarized:

$$
\ce{F^{\delta-}-H^{\delta+}}.
$$

The hydrogen atom retains a substantial positive charge and is directed toward the electron-rich benzene $\pi$ system.

The total fragment charges are

```text
Charge on HF      = -0.01291
Charge on C6H6    = +0.01291
```

Thus, approximately

$$
0.013e
$$

is transferred from benzene to HF.

The net direction of intermolecular charge transfer is therefore

$$
\ce{C6H6 -> HF}.
$$

The amount of transferred charge is small, as expected for a noncovalent complex.

---

### 15.2.5 H–F bonding NBO

The occupied H–F bonding orbital is

```text
11. (1.99896) BD (1) F 1-H 2
              (80.02%)  0.8945* F 1
              (19.98%)  0.4470* H 2
```

Its occupancy is

$$
n\left(\sigma_{\mathrm{H-F}}\right)=1.99896.
$$

The bonding NBO can be written approximately as

$$
\sigma_{\mathrm{H-F}} =
0.8945\,h_{\mathrm F}
+
0.4470\,h_{\mathrm H}.
$$

Because

$$
(0.8945)^2\approx0.8002,
$$

approximately $80.02\%$ of the bonding NBO is located on fluorine.

Only $19.98\%$ is located on hydrogen.

The H–F bond is therefore strongly polarized toward fluorine.

The fluorine natural hybrid contributing to the bond has the composition

```text
s(23.24%) p(76.57%)
```

and can be described approximately as an $sp^{3.29}$ hybrid.

The hydrogen contribution is almost entirely derived from its $1s$ orbital.

---

### 15.2.6 H–F antibonding NBO

The corresponding antibonding NBO is

```text
27. (0.01460) BD*(1) F 1-H 2
              (19.98%)  0.4470* F 1
              (80.02%) -0.8945* H 2
```

It can be written approximately as

$$
\sigma^\ast_{\mathrm{H-F}} =
0.4470\,h_{\mathrm F} -
0.8945\,h_{\mathrm H}.
$$

The antibonding NBO is polarized in the direction opposite to the bonding NBO:

| Orbital | F contribution | H contribution |
|---|---:|---:|
| $\sigma_{\mathrm{H-F}}$ | $80.02\%$ | $19.98\%$ |
| $\sigma^\ast_{\mathrm{H-F}}$ | $19.98\%$ | $80.02\%$ |

Thus, the largest part of the H–F antibonding orbital is located on the hydrogen atom.

This is important because the hydrogen end of HF points toward benzene. The large amplitude of $\sigma^\ast_{\mathrm{H-F}}$ on H allows effective overlap with the benzene $\pi$ system.

The antibonding occupancy is

$$
n\left(\sigma^\ast_{\mathrm{H-F}}\right)=0.01460.
$$

---

### 15.2.7 Second-order perturbation theory

The NBO second-order perturbation analysis examines interactions between occupied donor NBOs and unoccupied acceptor NBOs.

For a donor orbital $i$ and acceptor orbital $j$, the stabilization energy is approximately

$$ E^{(2)}_{i\rightarrow j}
= -q_i
\frac{F_{ij}^2}
{\varepsilon_j-\varepsilon_i},
$$

where:

- $q_i$ is the occupancy of the donor orbital;
- $\varepsilon_i$ and $\varepsilon_j$ are the donor and acceptor NBO energies;
- $F_{ij}$ is the off-diagonal Fock-matrix element.

A larger $E^{(2)}$ may result from:

- a highly occupied donor;
- a small donor–acceptor energy gap;
- a large donor–acceptor Fock-matrix coupling.

---

### 15.2.8 Main intermolecular interaction

The strongest intermolecular donor–acceptor interaction is

```text
22. BD (2) C 6-C 7  ->  27. BD*(1) F 1-H 2

E(2)          = 5.74 kcal mol-1
E(NL)-E(L)    = 0.75 a.u.
F(L,NL)       = 0.059 a.u.
```

`BD(2) C6-C7` is a localized benzene $\pi$-bonding NBO.

`BD*(1) F-H` is the H–F antibonding orbital.

The interaction is therefore

$$
\pi_{\mathrm{C6-C7}}
\rightarrow
\sigma^\ast_{\mathrm{H-F}}.
$$

This is the characteristic donor–acceptor interaction of an X–H···$\pi$ hydrogen bond.

The benzene $\pi$ system acts as the electron donor, while the H–F antibond acts as the electron acceptor.

The interaction has

$$
E^{(2)}=5.74\ \mathrm{kcal\,mol^{-1}},
$$

a donor–acceptor energy gap of

$$
\Delta\varepsilon=0.75\ E_{\mathrm h},
$$

and a Fock-matrix coupling of

$$
F_{ij}=0.059\ E_{\mathrm h}.
$$

---

### 15.2.9 Why does NBO identify only one C–C $\pi$ bond as the donor?

NBO represents the benzene $\pi$ system using one localized Kekulé structure containing three $\pi$ bonds.

For this calculation, one of the localized $\pi$ bonds is

```text
BD (2) C 6-C 7
```

The HF molecule is located closest to the C6–C7 region. Therefore, this localized $\pi$ NBO has the most favorable overlap with the H–F antibonding orbital.

The result should not be interpreted as meaning that benzene contains a permanently localized C6=C7 double bond.

The benzene $\pi$ electrons remain delocalized over the ring. The selected C6=C7 $\pi$ bond is only one component of the localized NBO representation.

The intermolecular interaction may therefore be written more generally as

$$
\pi_{\mathrm{benzene}}
\rightarrow
\sigma^\ast_{\mathrm{H-F}}.
$$

---

### 15.2.10 Smaller benzene-to-HF interactions

Two much smaller interactions into the H–F antibonding orbital are also found:

```text
BD (1) C 6-C 7  ->  BD*(1) F-H     0.06 kcal mol-1
BD (1) C 7-H 13 ->  BD*(1) F-H     0.06 kcal mol-1
```

These correspond to weak donation from the local $\sigma$ framework:

$$
\sigma_{\mathrm{C-C}}
\rightarrow
\sigma^\ast_{\mathrm{H-F}},
$$

and

$$
\sigma_{\mathrm{C-H}}
\rightarrow
\sigma^\ast_{\mathrm{H-F}}.
$$

Their stabilization energies are much smaller than that of the main interaction:

$$
5.74\ \mathrm{kcal\,mol^{-1}}
\gg
0.06\ \mathrm{kcal\,mol^{-1}}.
$$

The complex is therefore dominated by $\pi$ donation rather than by donation from the benzene $\sigma$ framework.

---

### 15.2.11 Weak back-donation from HF to benzene

A weak intermolecular interaction in the reverse direction is also present:

```text
LP (3) F 1  ->  BD*(2) C 6-C 7

E(2) = 0.22 kcal mol-1
```

This interaction corresponds to

$$
n_{\mathrm F}
\rightarrow
\pi^\ast_{\mathrm{C6-C7}}.
$$

The reverse interaction is considerably weaker than the forward interaction:

$$
E^{(2)} \left[ \pi_{\mathrm{benzene}} \rightarrow
\sigma^\ast_{\mathrm{H-F}} \right] =
5.74\ \mathrm{kcal\,mol^{-1}},
$$

whereas

$$ E^{(2)}
\left[ n_{\mathrm F} \rightarrow \pi^\ast_{\mathrm{benzene}}
\right] =
0.22\ \mathrm{kcal\,mol^{-1}}.
$$

Therefore,

$$
\pi_{\mathrm{benzene}}
\rightarrow
\sigma^\ast_{\mathrm{H-F}}
$$

is the dominant charge-transfer direction.

---

### 15.2.12 Effect of complex formation on the H–F bond

The H–F antibonding orbital has a nonzero occupancy:

$$
n\left(\sigma^\ast_{\mathrm{H-F}}\right)=0.01460.
$$

Population of an antibonding orbital opposes the bonding interaction. Therefore, donation from benzene into $\sigma^\ast_{\mathrm{H-F}}$ is expected to weaken the H–F bond.

The expected consequences are:

- a slight increase in the H–F bond length;
- a reduction in the H–F stretching frequency;
- a red shift of the H–F vibrational band;
- a reduction in the effective H–F bond order.

These effects should be established by comparison with an isolated HF molecule calculated using the same method and basis set.

In particular, one should compare:

$$ \Delta r_{\mathrm{H-F}} = r_{\mathrm{H-F}}(\text{complex}) - r_{\mathrm{H-F}}(\text{isolated}), $$

and

$$ \Delta\nu_{\mathrm{H-F}} = \nu_{\mathrm{H-F}}(\text{complex}) - \nu_{\mathrm{H-F}}(\text{isolated}). $$

A negative value of $\Delta\nu_{\mathrm{H-F}}$ would indicate a red shift.

The complete $\sigma^\ast_{\mathrm{H-F}}$ occupancy of $0.01460e$ should not automatically be assigned entirely to the intermolecular interaction because isolated HF may already possess a small nonzero antibonding occupancy.

The change in occupancy should therefore be calculated as

$$ \Delta n(\sigma^\ast_{\mathrm{H-F}}) = n(\sigma^\ast_{\mathrm{H-F}})_{\mathrm{complex}} - n(\sigma^\ast_{\mathrm{H-F}})_{\mathrm{isolated}}. $$

---

### 15.2.13 Polarization of the benzene ring

The natural charges on the carbon atoms are:

```text
C 3   -0.23853
C 4   -0.23759
C 5   -0.24071
C 6   -0.27733
C 7   -0.28404
C 8   -0.24060
```

The C6 and C7 atoms, which lie closest to the HF interaction region, have the most negative natural charges:

$$
q_{\mathrm{C6}}=-0.27733,
$$

and

$$
q_{\mathrm{C7}}=-0.28404.
$$

The remaining carbon charges lie approximately between

$$
-0.238
\quad\text{and}\quad
-0.241.
$$

This difference shows that HF polarizes the electron density of benzene near the C6–C7 interaction region.

However, atomic charges contain contributions from both:

- intramolecular polarization;
- intermolecular charge transfer.

Therefore, the more reliable measure of the net intermolecular charge-transfer direction is the fragment charge:

$$
\ce{C6H6^{+0.01291}\cdots HF^{-0.01291}}.
$$

---

### 15.2.14 Aromatic delocalization in benzene

NBO represents benzene using three localized $\pi$ bonds.

Their occupancies are approximately

```text
BD (2) C 3-C 8     1.65699
BD (2) C 4-C 5     1.65661
BD (2) C 6-C 7     1.67930
```

The corresponding $\pi^\ast$ occupancies are

```text
BD*(2) C 3-C 8     0.31659
BD*(2) C 4-C 5     0.31633
BD*(2) C 6-C 7     0.35054
```

A localized isolated double bond would ideally have approximately two electrons in the $\pi$-bonding NBO and little population in the corresponding $\pi^\ast$ NBO.

In benzene, the $\pi$-bond occupancies are considerably below $2e$, while the $\pi^\ast$ orbitals have substantial populations.

These occupancies arise from strong delocalization between alternative Kekulé structures.

Typical intramolecular interactions are

```text
pi(C-C) -> pi*(C-C)

E(2) approximately 19-21 kcal mol-1
```

For example:

```text
BD (2) C 3-C 8 -> BD*(2) C 4-C 5     20.17 kcal mol-1
BD (2) C 3-C 8 -> BD*(2) C 6-C 7     20.90 kcal mol-1
```

These large interactions are signatures of strong aromatic $\pi$ delocalization.

The HF molecule perturbs the ring and makes the three localized $\pi$ bonds slightly inequivalent, but it does not destroy the aromatic electronic structure.

---

### 15.2.15 Lewis and non-Lewis populations

For the complete complex, NBO reports:

```text
Total Lewis              50.77669  (97.647%)
Total non-Lewis           1.22331  ( 2.353%)
```

Thus, approximately $97.65\%$ of the electron population is assigned to the selected Lewis structure.

The non-Lewis population includes electron density in:

- the H–F antibonding orbital;
- benzene $\pi^\ast$ orbitals;
- C–C and C–H antibonding orbitals;
- Rydberg orbitals.

For the HF fragment:

```text
Total Lewis       9.99464  (99.8175%)
Valence non-Lewis 0.01460  ( 0.1458%)
Rydberg non-Lewis 0.00368  ( 0.0367%)
```

For the benzene fragment:

```text
Total Lewis       40.78205  (97.1300%)
Valence non-Lewis  1.14502  ( 2.7271%)
Rydberg non-Lewis  0.06002  ( 0.1429%)
```

The larger non-Lewis population of benzene mainly reflects its aromatic $\pi$ delocalization.

---

### 15.2.16 Why the NBO $E^{(2)}$ value is not the binding energy

The value

$$
E^{(2)}=5.74\ \mathrm{kcal\,mol^{-1}}
$$

is the perturbative stabilization associated with the specific interaction

$$
\pi_{\mathrm{C6-C7}}
\rightarrow
\sigma^\ast_{\mathrm{H-F}}.
$$

It is not the total binding energy of the benzene–HF complex.

The actual interaction energy contains several contributions:

- electrostatic attraction;
- induction and polarization;
- charge transfer;
- dispersion;
- exchange repulsion;
- deformation or geometry-relaxation energy;
- basis-set superposition error.

Therefore,

$$
E^{(2)} \neq \Delta E_{\mathrm{binding}}. $$

The binding energy should instead be evaluated from the total electronic energies of the complex and isolated fragments:

$$
\Delta E_{\mathrm{binding}} = E_{\mathrm{C_6H_6\cdots HF}} - E_{\mathrm{C_6H_6}} - E_{\mathrm{HF}}. $$

A counterpoise correction may also be used to estimate basis-set superposition error.

---

### 15.2.17 Recommended comparison with isolated HF and benzene

To quantify the changes caused by complex formation, perform separate NBO calculations for:

1. isolated HF;
2. isolated benzene;
3. the optimized benzene···HF complex.

The following quantities can then be compared:

| Quantity | Interpretation |
|---|---|
| $r_{\mathrm{H-F}}$ | H–F bond weakening or strengthening |
| $\nu_{\mathrm{H-F}}$ | Vibrational red or blue shift |
| $n(\sigma_{\mathrm{H-F}})$ | Change in bonding population |
| $n(\sigma^\ast_{\mathrm{H-F}})$ | Antibond population induced by complexation |
| $q_{\mathrm{HF}}$ | Net intermolecular charge transfer |
| Carbon natural charges | Polarization of the benzene ring |
| $\pi$ and $\pi^\ast$ occupancies | Perturbation of aromatic delocalization |
| Wiberg H–F bond index | Change in H–F bond order |
| Wiberg intermolecular indices | Degree of covalent character in the contact |

The most useful difference quantities are

$$ \Delta n(\sigma^\ast_{\mathrm{H-F}}) = n(\sigma^\ast_{\mathrm{H-F}})_{\mathrm{complex}} - n(\sigma^\ast_{\mathrm{H-F}})_{\mathrm{isolated}}, $$

and

$$ \Delta q_{\mathrm{HF}} = q_{\mathrm{HF}}(\mathrm{complex}) - q_{\mathrm{HF}}(\mathrm{isolated}). $$

---

### 15.2.18 Summary of the C<sub>6</sub>H<sub>6</sub>···HF NBO analysis

The main intermolecular orbital interaction is

$$
\boxed{
\pi_{\mathrm{benzene}}
\rightarrow
\sigma^\ast_{\mathrm{H-F}}
}
$$

| Quantity | Result |
|---|---:|
| Nature of complex | X–H···$\pi$ hydrogen-bonded complex |
| Molecular units | HF and C<sub>6</sub>H<sub>6</sub> |
| New covalent C–H bond | Not found |
| H–F bond length | Approximately $0.936$ Å |
| Position of H above ring plane | Approximately $2.20$ Å |
| Main donor | Benzene $\pi$ NBO |
| Main acceptor | $\sigma^\ast_{\mathrm{H-F}}$ |
| Main donor bond | Localized C6–C7 $\pi$ bond |
| Main $E^{(2)}$ | $5.74$ kcal mol$^{-1}$ |
| Donor–acceptor energy gap | $0.75$ a.u. |
| Fock-matrix coupling | $0.059$ a.u. |
| H–F bonding NBO occupancy | $1.99896$ |
| H–F antibonding NBO occupancy | $0.01460$ |
| Charge on F | $-0.59850$ |
| Charge on HF hydrogen | $+0.58559$ |
| Net charge transferred | Approximately $0.013e$ |
| Direction of charge transfer | Benzene $\rightarrow$ HF |
| Reverse $n_{\mathrm F}\rightarrow\pi^\ast$ interaction | $0.22$ kcal mol$^{-1}$ |
| Aromatic $\pi$ delocalization | Retained |
| NBO $E^{(2)}$ equal to binding energy | No |

The principal conclusions are:

1. HF and benzene remain separate molecular units.
2. No new covalent C–H bond is formed.
3. The positive hydrogen end of HF points toward the benzene $\pi$ system.
4. The dominant interaction is donation from benzene into the H–F antibonding orbital.
5. The primary donor–acceptor interaction is $\pi_{\mathrm{benzene}}\rightarrow\sigma^\ast_{\mathrm{H-F}}$.
6. Approximately $0.013e$ is transferred from benzene to HF.
7. The H–F antibonding orbital is strongly localized toward hydrogen, which favors overlap with the benzene $\pi$ cloud.
8. Population of $\sigma^\ast_{\mathrm{H-F}}$ is expected to weaken and red-shift the H–F bond.
9. Reverse donation from fluorine into benzene is very small.
10. The aromatic $\pi$ system of benzene remains strongly delocalized.
11. The $E^{(2)}$ value of $5.74$ kcal mol$^{-1}$ describes one orbital interaction and is not the total binding energy of the complex.
