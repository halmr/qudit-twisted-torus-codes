# qudit-twisted-torus-codes

Code accompanying

> M. Halla, *Qudit Twisted-Torus Codes in the Bivariate Bicycle Framework*,
> arXiv:2602.04443 — https://arxiv.org/abs/2602.04443

It searches for weight-6 qudit CSS codes of generalized-toric (bivariate bicycle)
type on twisted tori over the finite field F_q (q = 3, 5, 7), computes their
number of logical qudits with Gröbner bases, and estimates their distance with
QDistRnd.

## Requirements

Tested with

- SageMath 10.9 (Python 3.12) — search notebook
- GAP 4.15.1 with QDistRnd 0.9.5 (Jupyter GAP kernel) — distance notebook
- Python 3.11 with pandas — selection notebook

## Workflow

1. `sage_search_qudit_twisted_torus_codes.ipynb` — set q, k_target, num_fg, max_exp
   and the list of block lengths n. Writes, for each n,
   `data/data_{n}n_{k}k_{q}q_{w}w/minus_n{n}fg_{k}k_{q}q_{w}wait.csv`
   (the sampled pairs (f, g) and tori (alpha, beta, gamma) with exactly
   k logical qudits).
2. `gap_twisted_torus_distance.ipynb` — set q, k_tg, num (information sets) and
   the same list of n. Reads the `minus_` files and writes `dis_n{n}_...csv`
   with the estimated distance on the twisted torus (d) and on the untwisted
   one (d0). The values returned by QDistRnd are upper bounds on the true
   distances.
3. `select_best_codes.ipynb` — ranks the codes of one n by k d²/n, ties broken
   by the smallest stabilizer range, and prints the best ones.

## Example

The folder `data/data_42n_4k_3q_6w` contains the CSV files of steps 1 and 2
for q = 3, k = 4, n = 42; running step 3 on it reproduces the entry below.
The best code found is [[42,4,8]]_3 with
f = 1 + y^-2 + x^-1*y^-2, g = x^2*y + 1 + x^-1*y^-3 on the torus
a1 = (0,3), a2 = (7,-2), k d²/n = 6.10 (Table 1 of the paper).
On the untwisted torus a2 = (7,0) the same f, g give only k = 2 and d = 7.

## Citation

If you use this code or the codes found with it, please cite the paper above
(see `CITATION.cff`).

## License

MIT — see `LICENSE`.
