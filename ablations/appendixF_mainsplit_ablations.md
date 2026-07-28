# Appendix F ablations re-run on the main validated Neon split (M2AB, 2026-07-26)

18 single-parameter variants of `m2_neon_cs_full_s0` (identical recipe, seed 0, main validated
split, test-25). Base = m2 3-seed run (32.708/32.748/32.764, sigma=0.03). Screen = the paper's
80/5/14 30-epoch Appendix F values.

## Experiment 1: local geometry encoder

| Variant | screen RMSE (80/5/14) | main-split RMSE | delta vs base |
|---|---|---|---|
| encoder slices 32 | 36.707 | 32.658 | -0.050 |
| baseline | 37.135 | 32.708 | +0.000 |
| encoder layers 3 | 37.612 | 32.720 | +0.012 |
| encoder slices 8 | 37.165 | 32.734 | +0.026 |
| encoder layers 1 | 36.892 | 32.758 | +0.050 |

## Experiment 2: global mixer

| Variant | screen RMSE (80/5/14) | main-split RMSE | delta vs base |
|---|---|---|---|
| global heads 8 | 37.136 | 32.667 | -0.041 |
| global layers 3 | 36.919 | 32.675 | -0.033 |
| global heads 2 | 37.118 | 32.676 | -0.032 |
| global layers 1 | 36.987 | 32.690 | -0.018 |
| baseline | 37.135 | 32.708 | +0.000 |

## Experiment 3: capacity

| Variant | screen RMSE (80/5/14) | main-split RMSE | delta vs base |
|---|---|---|---|
| decoder hidden 128 | 37.724 | 32.127 | -0.581 |
| decoder hidden 384 | 37.240 | 32.661 | -0.047 |
| latent dim. 192 | 37.610 | 32.692 | -0.016 |
| baseline | 37.135 | 32.708 | +0.000 |
| latent dim. 96 | 36.951 | 32.766 | +0.058 |

## Experiment 4: conditioning / part information

| Variant | screen RMSE (80/5/14) | main-split RMSE | delta vs base |
|---|---|---|---|
| contact tokens 16 | 37.074 | 32.681 | -0.027 |
| baseline | 37.135 | 32.708 | +0.000 |
| contact tokens 0 | 37.233 | 32.721 | +0.013 |
| positional dim. 32 | 37.156 | 32.728 | +0.020 |
| part embedding 8 | 37.010 | 32.745 | +0.037 |
| positional dim. 8 | 37.193 | 32.793 | +0.085 |
| part embedding 32 | 36.983 | 32.907 | +0.199 |

## Transfer verdict

- 16/18 variants within +-0.09 mm of base (<=0.3%; seed sigma 0.03): architecture robust to these choices at main-split scale.
- Fine-grained screen rankings do NOT all transfer: screen-best partemb32 (Exp 4) is main-split WORST (+0.199 mm ~ 6 sigma); screen-best latent096 (Exp 3) is slightly negative (+0.058).
- Only clear main-split win: dec128 (-0.581 mm ~ 19 sigma; 32.13 mm) — screen ranked it worst in Exp 3. Moderate capacity regularizes better at this data scale.
- Exp 1 best (slices32) replicates on both splits; Exp 2 remains insensitive on both.
