# Meeting 02.09.2026

SIPRI Arms Transfers Database, 1950–2024 · directed weighted order-year network:
15,264 annual dyad edges, 195 countries.

## 1. LAGO

**Resolved:** the window problem. Years form the time axis directly, no window
width to choose, no post-hoc Jaccard stitching. Community identity follows from
the optimisation rather than being assigned afterwards.

**Not resolved:** the core-periphery structure.

| Diagnostic | Result |
|---|---|
| Baseline (MM, γ=1, ω=2) | 22 modules, L-Modularity 0.3385 |
| Parameter sensitivity | 8–232 modules, no plateau |
| Three restarts, same settings | 19 / 35 / 20 modules, mean ARI **0.276** |
| Leading supplier's share of internal TIV | 93–98% (USSR 1964, 1984; Russia 2024) |

The instability is a property of the data, not the settings. Modularity, including L-Modularity, tests for **assortative** structure, groups dense
internally. This network is **disassortative**: members of a detected community
trade with the centre, not with each other. LAGO recovers supplier clienteles, not blocs.

## 2. Exploratory analysis: supplier structure

Each recipient assigned to the supplier it bought most from that year. No
optimisation, no parameters, reproducible by construction.

**Recipients depend on one source.** Mean dependence on the largest supplier is
0.83–0.92 across the period; 38–57% of recipients have a single supplier at all.

**Clientele sizes track the historical record** (recipients whose largest
supplier this was):

| Supplier | 1964 | 1984 | 1999 | 2024 |
|---|---|---|---|---|
| United States | 32 | 34 | 22 | 32 |
| Soviet Union | 21 | 26 | — | — |
| Russia | — | — | 10 | 4 |
| France | 15 | 20 | 8 | 6 |
| United Kingdom | 14 | 10 | 9 | 1 |
| China | 1 | 2 | 3 | 5 |

**Out-in degree assortativity is negative in every one of the 75 years**
(−0.02 to −0.35): large exporters trade with small importers, not with each other.

**Against expectation:** suppliers grew from 22 to 45 and the top-three TIV share
fell from 0.90 to 0.67, yet recipient dependence did not fall. The market
diversified on the selling side while the periphery stayed tied to single sources.

## 3. Proposed next step

The structure is stable and measurable — it is core-periphery rather than modular.
Established core-periphery detection is undirected, which would collapse the
supplier/recipient distinction that matters most here.

> Elliott, Chiu, Bazzi, Reinert & Cucuringu (2020). Core–periphery structure in
> directed networks. *Proc. R. Soc. A* 476(2241), 20190783.
> [doi](https://doi.org/10.1098/rspa.2019.0783) ·
> [arXiv:1912.00984](https://arxiv.org/abs/1912.00984)

Direction-dependent core and periphery sets: separate cores on the selling and
buying side. One of their three applications is a trade network. No released
implementation; the spectral methods would have to be written from the paper.

**Open question.** Before committing to that, we would like to settle the final
aim of the project: is the deliverable community detection, or a characterisation
of the structure by other means? The answer changes what is worth building.

## Files

`lago.ipynb` — LAGO pipeline, sensitivity, restart stability
`supplier_structure.ipynb` — supplier-clientele analysis

```bash
pip install "dcd-lago==1.1.0" pandas numpy scikit-learn matplotlib networkx
```

`dcd-lago` requires Python ≥ 3.11. Both notebooks take the SIPRI CSV as their only input.
