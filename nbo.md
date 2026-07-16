# 15. NBO Analysis with NBO 7.0 and ORCA 6.1.1

Natural Bond Orbital analysis transforms molecular orbitals into localized orbitals that resemble familiar chemical objects such as bonds, lone pairs, antibonding orbitals, and Rydberg orbitals.

The hydrogen molecule is the simplest possible example because it contains only:

- one occupied H–H bonding orbital;
- one corresponding H–H antibonding orbital;
- no lone pairs;
- no core orbitals;
- no significant donor–acceptor delocalization.

---

## 15.1 NBO analysis of the H$_2$ molecule

### 15.1.1 Optimized geometry

The optimized geometry is stored in `opt.xyz`.

```text
2
Coordinates from ORCA-job opt E  -1.172052706418
  H           0.00000000000000      0.00000000000000      0.12859575544094
  H           0.00000000000000      0.00000000000000      0.87140424455906
```

The molecule lies along the $z$-axis. The two H atoms are symmetry equivalent.

---

### 15.1.2 ORCA input for NBO analysis

The NBO calculation is performed using the following input.

```text
! B3LYP 6-31+G(d,p) def2/J RIJCOSX TightSCF NBO

* xyzfile 0 1 opt.xyz

%base "nbo"

```

The important keywords are:

| Keyword | Meaning |
|---|---|
| `B3LYP` | Density functional used for the electronic-structure calculation |
| `6-31+G(d,p)` | Orbital basis set |
| `def2/J` | Auxiliary basis used for the Coulomb-fitting approximation |
| `RIJCOSX` | Efficient approximation for Coulomb and exchange terms |
| `TightSCF` | Tightens the SCF convergence criteria |
| `NBO` | Requests an NBO analysis |
| `%base "nbo"` | Sets the base name of the output and associated files |

---

## 15.2 Natural Atomic Orbitals and Natural Population Analysis

The first important section is:

```text
NATURAL POPULATIONS: Natural atomic orbital occupancies
```

For the first H atom, NBO reports:

```text
1    H  1  s      Val( 1s)     0.99923
5    H  1  pz     Ryd( 2p)     0.00077
```

For the second H atom:

```text
6    H  2  s      Val( 1s)     0.99923
10   H  2  pz     Ryd( 2p)     0.00077
```

Each H atom therefore has a total electron population of

$$
0.99923+0.00077=1.00000.
$$

The natural charge is defined as

$$
q_A=Z_A-N_A,
$$

where $Z_A$ is the nuclear charge and $N_A$ is the natural electron population.

For each H atom,

$$
q_{\mathrm H}=1-1=0.
$$

The output confirms this:

```text
Summary of Natural Population Analysis:

Atom No    Natural Charge
H  1          0.00000
H  2          0.00000
```

Thus, NPA assigns exactly one electron to each H atom. This is expected for a homonuclear molecule with two symmetry-equivalent atoms.

### Small $p_z$ contribution

The H–H bond is not constructed from perfectly pure $1s$ functions. The basis set contains polarization functions, so the occupied bond contains a very small amount of $p_z$ character.

The total Rydberg population is

```text
Natural Rydberg Basis      0.00155  (0.0773% of 2)
```

This is extremely small. The H–H bond is therefore almost entirely a $1s$–$1s$ bond.

---

## 15.3 Lewis structure selected by NBO

The NBO program searches for a localized Lewis structure. For H$_2$, it finds:

```text
CR  0
BD  1
nC  0
LP  0
```

These labels mean:

| Label | Meaning | Number in H$_2$ |
|---|---|---:|
| `CR` | Core orbital | 0 |
| `BD` | Two-center bonding orbital | 1 |
| `nC` | One-center nonbonding orbital | 0 |
| `LP` | Lone pair | 0 |

Therefore, the NBO Lewis structure is simply

$$
\mathrm{H-H}.
$$

The output also shows:

```text
Total Lewis       2.00000  (100.000%)
Total non-Lewis   0.00000  (0.000%)
```

Both electrons are assigned to the H–H bonding NBO. There is no electron population in separate antibonding or Rydberg NBOs.

---

## 15.4 H–H bonding NBO

The occupied bonding NBO is printed as:

```text
1. (2.00000) BD ( 1) H  1- H  2
             ( 50.00%)   0.7071* H  1 s( 99.92%)p 0.00(  0.08%)
             ( 50.00%)   0.7071* H  2 s( 99.92%)p 0.00(  0.08%)
```

The occupancy is

$$
n[\mathrm{BD(H-H)}]=2.00000.
$$

The bonding NBO can be written as

$$
\mathrm{BD(H-H)}=0.7071\,h_{\mathrm{H1}} + 0.7071\,h_{\mathrm{H2}},$$

where $h_{\mathrm{H1}}$ and $h_{\mathrm{H2}}$ are the natural hybrids on the two H atoms.

Because

$$
(0.7071)^2=0.5000,
$$

each H atom contributes $50\%$ to the bond.

This is a perfectly nonpolar covalent bond.

For a heteronuclear bond, the two coefficients would generally be different. The larger squared coefficient would indicate the atom toward which the bonding orbital is polarized.

---

## 15.5 Composition of the hydrogen natural hybrids

Each H hybrid is reported as

```text
s(99.92%) p(0.08%)
```

The natural hybrid on H1 is approximately

$$
h_{\mathrm{H1}}
= 0.9996(1s_{\mathrm{H1}})
+
0.0278(p_{z,\mathrm{H1}}),
$$

while the hybrid on H2 is approximately

$$
h_{\mathrm{H2}}
= 0.9996(1s_{\mathrm{H2}}) -
0.0278(p_{z,\mathrm{H2}}).
$$

The opposite signs of the $p_z$ coefficients arise because the two H atoms lie on opposite sides of the molecular center. The two natural hybrids point toward each other.

The H–H bond is therefore essentially a $1s$–$1s$ bond with a very small polarization contribution.

In conventional molecular-orbital language, this bonding NBO corresponds closely to the occupied

$$
\sigma_g(1s)
$$

orbital of H$_2$.

---

## 15.6 H–H antibonding NBO

The corresponding antibonding orbital is:

```text
2. (0.00000) BD*( 1) H  1- H  2
             ( 50.00%)   0.7071* H  1
             ( 50.00%)  -0.7071* H  2
```

It can be written as

$$
\mathrm{BD^\ast(H-H)} =
0.7071\,h_{\mathrm{H1}} -
0.7071\,h_{\mathrm{H2}}.
$$

The minus sign produces destructive interference and a node between the two H nuclei.

In molecular-orbital language, this orbital corresponds closely to

$$
\sigma_u^\ast(1s).
$$

Its occupancy is

$$
n[\mathrm{BD^\ast(H-H)}]=0.00000.
$$

Thus, the closed-shell ground state contains two bonding electrons and no antibonding electrons.

The corresponding simple bond order is

$$
\text{bond order} =
\frac{n_{\mathrm{bonding}}-n_{\mathrm{antibonding}}}{2} =
\frac{2-0}{2} =
1.
$$

---

## 15.7 Why is there a small Rydberg NAO population but zero Rydberg NBO occupancy?

At the NAO level, each H atom has a small $p_z$ population:

```text
H  1  pz  Ryd(2p)  0.00077
H  2  pz  Ryd(2p)  0.00077
```

However, the separately listed Rydberg NBOs have zero occupancy:

```text
RY (1) H 1   0.00000
RY (2) H 1   0.00000
...
```

These statements are not contradictory.

The small $p_z$ contribution is incorporated into the occupied natural hybrids that form the H–H bond. It represents slight polarization of the bonding orbital.

The separately listed Rydberg NBOs are orthogonal, unoccupied orbitals.

Therefore,

$$
\text{small Rydberg NAO population}
\neq
\text{occupied Rydberg NBO}.
$$

---

## 15.8 NHO directionality and bond bending

The output reports:

```text
NHO DIRECTIONALITY AND BOND BENDING
None exceeding thresholds
```

This means that NBO finds no significant bending of the natural hybrids away from the H–H internuclear axis.

This is expected because:

- H$_2$ is linear;
- the two hybrids point directly toward each other;
- the $p$-character is extremely small.

---

## 15.9 Second-order perturbation theory analysis

The output reports:

```text
SECOND ORDER PERTURBATION THEORY ANALYSIS OF FOCK MATRIX IN NBO BASIS

None above threshold
```

Second-order NBO analysis identifies interactions between an occupied donor NBO and an unoccupied acceptor NBO, for example:

$$
\mathrm{LP}\rightarrow\mathrm{BD^\ast},
$$

$$
\mathrm{BD}\rightarrow\mathrm{BD^\ast},
$$

or

$$
\pi\rightarrow\pi^\ast.
$$

H$_2$ has only one occupied Lewis NBO:

$$
\mathrm{BD(H-H)}.
$$

It has no lone pairs, neighboring bonds, or other occupied donor orbitals. Therefore, there is no additional donor–acceptor delocalization.

The H–H bond itself is already represented directly as the occupied bonding NBO. Bond formation is not treated as a second-order donor–acceptor interaction.

Therefore,

$$
\text{H-H bond formation}
\neq
\mathrm{BD(H-H)}\rightarrow\mathrm{BD^\ast(H-H)}
\text{ delocalization}.
$$

---

## 15.10 NBO orbital energies

The NBO summary gives:

```text
BD (1) H 1-H 2      occupancy 2.00000    energy -0.42804 a.u.
BD*(1) H 1-H 2      occupancy 0.00000    energy  0.38589 a.u.
```

The bonding NBO is lower in energy, while the antibonding NBO is higher in energy.

The NBO orbital-energy separation is

$$
\Delta\varepsilon = \varepsilon_{\mathrm{BD^\ast}}
- \varepsilon_{\mathrm{BD}}.
$$

These orbital energies are diagonal Fock-matrix elements in the NBO representation.

They are not:

- the total molecular energy;
- the H–H bond dissociation energy;
- an exact electronic excitation energy.

A real electronic excitation also includes orbital relaxation and electron–electron interaction effects.

---

## 15.11 Meaning of the `$CHOOSE` section

At the end of the NBO output, the program prints:

```
$CHOOSE
  BOND S 1 2 END
$END
```

This is the compact NBO specification of the selected Lewis structure.

`BOND S 1 2` means:

- a single bond;
- between atoms 1 and 2.

Thus, the selected Lewis structure is H–H.

---

## 15.12 Summary of the H$_2$ NBO analysis

The complete NBO description is

$$
\boxed{ \mathrm{H_2} =
\mathrm{BD(H-H)}^2
}
$$

with

$$
\mathrm{BD(H-H)}
\approx
\frac{1}{\sqrt{2}}
\left(
1s_{\mathrm{H1}}+1s_{\mathrm{H2}}
\right),
$$

and

$$
\mathrm{BD^\ast(H-H)}
\approx
\frac{1}{\sqrt{2}}
\left(
1s_{\mathrm{H1}}-1s_{\mathrm{H2}}
\right).
$$

| Quantity | Result |
|---|---:|
| Natural charge on H1 | 0.00000 |
| Natural charge on H2 | 0.00000 |
| H1 contribution to the bond | 50.00% |
| H2 contribution to the bond | 50.00% |
| Bonding NBO occupancy | 2.00000 |
| Antibonding NBO occupancy | 0.00000 |
| Lewis population | 100.000% |
| Non-Lewis population | 0.000% |
| Bond order | 1 |
| Significant donor–acceptor interactions | None |

The main conclusions are:

1. H$_2$ contains one perfectly occupied two-center H–H bonding NBO.
2. The bond is shared equally between the two H atoms.
3. The corresponding antibonding NBO is empty.
4. The H–H bond is almost entirely formed from hydrogen $1s$ orbitals.
5. The small $p_z$ contribution represents polarization of the occupied bond.
6. There are no significant second-order donor–acceptor interactions.
7. NBO therefore gives an almost ideal Lewis description of H$_2$.

> **Important limitation:** This simple closed-shell picture is appropriate near the equilibrium H–H distance. At very large H–H separation, a restricted closed-shell calculation does not correctly describe two separated open-shell H atoms.
