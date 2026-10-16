# SSH chain band gap: tight-binding simulation

Hyosan Shin · PHY4008 Computational Physics · Midterm project (presentation date: 2026-10-13)

Course companion to the slides in [`slides/SSH_band_gap_midterm.pptx`](slides/SSH_band_gap_midterm.pptx) (13 main slides and 3 backup slides).

## Motivation and physics question

Placing atoms in a line turns their energy levels into bands, and the empty energy range between two bands (the band gap) separates metals from semiconductors. A chain whose bonds are alternately short and long (as in polyacetylene) has such a gap, and the simplest model of it is the SSH (Su–Schrieffer–Heeger) chain. This project simulates the electron energies of this chain with a tight-binding model.

> How does the band gap of the SSH chain change with t2/t1, and how well does a finite-chain numerical calculation converge to it?

Quantities: the bands E±(k) and the gap, the lowest bulk |E| of an open chain (convergence to the gap), and, as a preliminary observation only, the number and location of states inside the gap of a finite chain.

**Result (checked numerically):** the gap is `E_gap = 2|t1 − t2|`, it closes at t1 = t2, the numerical results agree with exact results to about 1e-15, and the error of the finite-chain gap decreases as 1/N_c² (N_c: number of unit cells). A finite chain with t2 > t1 has two states inside the gap, located at the two ends. This last item is an observation and is not explained here.

## Model, assumptions, boundary conditions

- Unit cell with two atoms A and B; hopping energy t1 inside a cell and t2 between cells (arbitrary units).
- Assumptions: nearest-neighbor hopping only, orthogonal orbitals, no on-site energy, lattice constant a = 1, hbar = 1.
- Periodic boundary conditions for bands, the Bloch Hamiltonian and rings; open boundary conditions for the finite chain.
- Convention: the finite chain starts at atom A and its first bond is t1 (changing this swaps which chain has the in-gap states).

## Numerical method

Matrix diagonalization (`numpy.linalg.eigvalsh` / `eigh`): a 2×2 matrix at every k, and a 2N_c × 2N_c matrix for the open chain. The matrices are small, so the result is exact up to machine precision and there is no step size to converge. No random numbers are used, so every run gives the same result.

## What the main quantities mean (plain language)

| Symbol | Meaning |
|---|---|
| t1, t2 | hopping energies: how strongly an electron is coupled to its neighbor inside / between unit cells |
| k | wavenumber: a label for the electron states of a periodic chain (unit 1/length) |
| h(k) = t1 + t2 e^(ika) | coupling between A and B summed over cells; the two band energies are +|h| and −|h| |
| E_gap | lower edge of the upper band minus upper edge of the lower band |
| N_c, N_k, N | number of unit cells, number of k points, number of atoms in a ring |

## Presentation structure

| Slides | Part |
|---|---|
| 1–3 | Title, motivation, question and quantities |
| 4–7 | Model, gap formula from the references, quantities computed, numerical workflow |
| 8–10 | Results and validation (gap vs t2, comparison with exact results, resolution) |
| 11–13 | Interpretation (as explained in the references), limitations, summary |
| 14–16 | Backup: gap formula, monatomic chain, reproducibility and sources |

## Environment and dependencies

Python 3.12, packages pinned in `requirements.txt` (numpy 2.4.4, matplotlib 3.10.8, ipykernel 7.4.0, nbformat 5.11.1, nbclient 0.11.0, nbconvert 7.17.1).

## How to run

1. Install: `python -m pip install -r requirements.txt` (and `jupyterlab` if you want to edit the notebook).
2. Notebook: open `tight_binding.ipynb`, use **Restart Kernel and Run All** (about 10 s).
3. Script: `python project.py` writes the same tables and figures to `output/`.
4. No random numbers are used, so every run gives the same result. `index.html` is a static copy of the executed notebook.

```
midterm-tight-binding/
├── README.md
├── tight_binding.ipynb       # executed notebook
├── project.py                # script generated from the notebook
├── index.html                # static copy of the notebook
├── requirements.txt
├── manifest.json             # SHA-256 checksum of every file
├── provenance.json
├── input/params.json         # every setting
├── output/                   # csv tables, summary.json, figs/
└── slides/                   # deck and the images it uses
```

## Inputs and parameters

All settings are in `input/params.json` (created from defaults if missing): the hopping pairs (t1, t2) for the bands and the gap table, the t2 scan range for the gap, the number of unit cells of the open chain and the threshold for in-gap states (|E| < 0.1), and the lists of N_k, ring sizes and chain lengths for the resolution tests.

## How to reproduce the figures

| File | Content | Notebook section |
|---|---|---|
| `fig1_monatomic.png` | monatomic chain: analytic vs diagonalization | 1 |
| `fig2_ring_check.png` | ring of 20 atoms vs analytic E(k) | 5-1 |
| `fig3_bands_compare.png` | SSH bands for (1, 0.5) and (0.5, 1) | 2 |
| `fig4_gap_vs_t2.png` | gap vs t2 | 3 |
| `fig6_edge_states.png` | finite-chain levels and weights of the states closest to E = 0 | 4 |
| `fig8_resolution.png` | errors vs N_k, ring size and chain length | 5-2 |

Slides 2, 4 and 11 use schematics (`fig_levels_N`, `fig_dimerization`, `fig_ssh_chain`, `fig_folding`) that are not simulation output. The equations on the slides are typeset images embedded in the deck.

## Validation and limitations

| Check | Result |
|---|---|
| Ring of 20 atoms vs analytic E(k) = −2t cos(ka) | max difference 1.1e-15 |
| SSH 2×2 energies vs ±|h(k)| | max difference 2.2e-16 |
| Gap vs 2|t1 − t2| over the t2 scan | max difference 2.4e-16 |
| t1 = t2: SSH ring vs monatomic ring | difference 0 |
| t2 → 0 (isolated A–B pairs) | all |E| = t1 |
| t1 → 0 (end atoms decouple) | two E = 0 states, end-site weight 1.0 |

Error definitions: ring, SSH and gap: maximum over all levels of |numerical − analytic|; k grid: gap computed on the grid minus the exact gap 2|t1 − t2|; ring size: 2t minus the largest eigenvalue; chain length: lowest bulk |E| minus |t1 − t2| (for t2 > t1 the two in-gap states are skipped).

Resolution (t1, t2) = (1, 0.5): with an even number of k points the grid contains k = π and the gap error is 0; with an odd number it is skipped (error +0.033 at N_k = 17, +0.009 at 33). For the open chain the error is 0.033, 0.010, 0.0028, 0.00073, 0.00019 at N_c = 10, 20, 40, 80, 160, a log–log slope of about −1.9, consistent with 1/N_c² (second-order expansion of |h| near k = π/a, coefficient 4.93, measured 4.8 at N_c = 160).

| Not done / limitation | How to check |
|---|---|
| Real polyacetylene hopping values are not used | repeat with literature t1, t2 and compare with the measured gap |
| Chain length N_c ≤ 160; small gaps are not yet asymptotic | longer chains, check the 1/N_c² trend |
| Why the in-gap states appear | outside this project: analyze their amplitudes, length dependence and symmetry |
| 2D (graphene), electron–electron interaction | outside this model |

## References and AI assistance

**References** (numbers match the slides)

1. W. P. Su, J. R. Schrieffer, A. J. Heeger, Solitons in polyacetylene, Phys. Rev. Lett. 42, 1698 (1979).
2. N. W. Ashcroft, N. D. Mermin, Solid State Physics (1976): Ch. 8 (Bloch's theorem), Ch. 10 (the tight-binding method).
3. J. K. Asbóth, L. Oroszlány, A. Pályi, A Short Course on Topological Insulators, Lecture Notes in Physics 919 (Springer, 2016), arXiv:1509.02295, Ch. 1.
4. R. E. Peierls, Quantum Theory of Solids (Oxford University Press, 1955).

Derived in this project, not taken from a reference: the error definitions and the 1/N_c² error scaling.

**AI assistance:** Claude (Anthropic) was used for the code, validation checks, README and slide design. The formulas are taken from the cited references and checked numerically with the code.
