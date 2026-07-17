# 15. NBO Analysis with NBO 7.0 and ORCA 6.1.1

Natural Bond Orbital analysis provides a localized description of the electronic structure obtained from a quantum-chemical calculation. Instead of describing the molecule only in terms of delocalized canonical molecular orbitals, NBO constructs chemically intuitive orbitals such as:

- core orbitals (`CR`);
- two-center bonding orbitals (`BD`);
- antibonding orbitals (`BD*`);
- lone-pair orbitals (`LP`);
- lone vacancies (`LV`);
- Rydberg orbitals (`RY`).

NBO analysis can be used to examine:

- natural atomic charges and electron populations;
- bond polarization and hybridization;
- bonding and antibonding orbital occupancies;
- Lewis and non-Lewis electron populations;
- donor–acceptor interactions;
- hyperconjugation and resonance;
- hydrogen bonding and other noncovalent interactions;
- charge transfer between molecular fragments.

A commonly used measure of donor–acceptor interaction is the second-order perturbative stabilization energy,

$$
E^{(2)}_{i\rightarrow j} = -q_i \frac{F_{ij}^{\,2}} {\varepsilon_j-\varepsilon_i},
$$

where $q_i$ is the donor occupancy, $\varepsilon_i$ and $\varepsilon_j$ are the donor and acceptor NBO energies, and $F_{ij}$ is their off-diagonal Fock-matrix coupling.

The examples in this section increase gradually in complexity:

1. H<sub>2</sub>, which illustrates the simplest bonding and antibonding NBOs;
2. C<sub>6</sub>H<sub>6</sub>···HF, which illustrates an intermolecular $\pi\rightarrow\sigma^\ast$ hydrogen-bonding interaction;
3. additional systems illustrating lone-pair donation, hyperconjugation, resonance, and $n\rightarrow\pi^\ast$ interactions.

The calculations are performed with ORCA 6.1.1, while the localized orbital analysis is carried out using NBO 7.0.
