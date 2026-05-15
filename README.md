# Hitag2 Correlation Attack

Reproduction in pure Python of the fast correlation attack on the
Hitag2 stream cipher described in Garcia, Oswald, Kasper & Pavlidis,
*"Lock It and Still Lose It — On the (In)Security of Automotive
Remote Keyless Entry Systems"* (USENIX Security 2016), implemented as
a self-contained Google Colab notebook for the CPS and IoT Security
course.

The full write-up — methodology, results, and discussion of the
discrepancies with the paper's C implementation — is in
[`report_hitag2.pdf`](report_hitag2.pdf).

## Repository layout

```
.
├── Hitag2_project.ipynb   # full implementation + experiments
├── lfsr_diagram.png       # LFSR / nonlinear filter f20 schematic
├── rank_vs_round.png      # correlation-attack convergence plot
└── report_hitag2.pdf      # final report
```

## How to run

The notebook was developed and executed on **Google Colab (free tier)**
with Python 3.10 and NumPy. To reproduce:

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/riccardopivato/hitag2-correlation-attack/blob/main/Hitag2_project.ipynb)

or open the notebook manually in Colab via *File → Open notebook →
GitHub → riccardopivato/hitag2-correlation-attack*.

The notebook is self-contained: no external dataset, no hardware, no
RF interception is required. Every Hitag2 trace is generated inside
the notebook from a freshly seeded LFSR, so the attack can be
validated independently of the physical key-fob hardware.

## Notebook structure

The notebook is organised in three blocks:

1. **Cipher simulation** — defines `f20`, the LFSR feedback, and the
   keystream generator, matching the paper's Definitions 4.1–4.3.
2. **Reference correlation attack** — implements the algorithm as
   described in the paper, prioritising readability and 1:1
   correspondence with the pseudocode. Not intended to terminate on
   Colab (estimated runtime: hours to days); serves as algorithmic
   documentation.
3. **Optimised correlation attack** — pre-computed `bit_score` lookup
   tables and other optimisations to make the attack feasible within
   Colab's time and memory limits.

## References

- [1] F.D. Garcia, D. Oswald, T. Kasper, P. Pavlidis. *"Lock It and
  Still Lose It — On the (In)Security of Automotive Remote Keyless
  Entry Systems."* 25th USENIX Security Symposium, 2016.
- [2] A. Verstegen. *Hitag2 pseudocode.*
  github.com/factoritbv/hitag2hell/tree/master/pseudocode

See `report_hitag2.pdf` for the full discussion.
