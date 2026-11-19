# Reproducing TRAK on CIFAR-10

Student project for the course *Fundamentals of reproducible research and free software* (MVA, ENS Paris-Saclay, 2026-2027).
Authors: Salomé Fonvielle, Rémi Moysan, Jeanne Treyer.

We study the reproducibility of [TRAK](https://github.com/MadryLab/trak), a data attribution library developed at the Madry Lab (MIT), described in:

> S. M. Park, K. Georgiev, A. Ilyas, G. Leclerc, A. Madry. *TRAK: Attributing Model Behavior at Scale.* ICML 2023. [arXiv:2303.14186](https://arxiv.org/abs/2303.14186)

## Contents

| Path | Description |
|---|---|
| `notebook/TRAK_reproducibility_experiment.ipynb` | Our run of the authors' CIFAR-10 quickstart notebook, with outputs. Section 0 (installation) and all comments are ours; the rest is the authors' code, unchanged. |
| `patches/fast_jl_arch_7.5.patch` | The one-line change we applied to `fast_jl/setup.py` so that it builds with CUDA 13. |
| `environment.md` | The exact environment used for our run. |
| `report/` | LaTeX sources of our report. |

## How to rerun the experiment

1. Open the notebook in [Google Colab](https://colab.research.google.com/drive/1koIoSs9hyIWqVHzmL8bm13kDCPJLiHgz?usp=sharing) (or upload it), and select a GPU runtime.
2. Run all cells. Section 0 installs TRAK and fixes its GPU module:
   - the documented command `pip install traker[fast]` fails on a current environment;
   - `fast_jl` is built with `--no-build-isolation` (it needs PyTorch at build time but does not declare it);
   - the hard-coded GPU architecture 7.0, no longer supported by CUDA 13, is replaced by 7.5 (see `patches/`). Adapt this value to your GPU.
3. The notebook downloads CIFAR-10 from its original server, and the authors' reference results (for the LDS) from Dropbox. Neither is redistributed here.

Note that no random seed is set in the authors' notebook: results may vary slightly between runs.

## Results (run of November 18, 2026)

- Test accuracy of the ResNet-9: **91.8%**
- Linear Datamodeling Score (LDS): **0.090** (average p-value 0.003), with a single training run and 5 checkpoints

## Licenses

- Our code and notebook: MIT License (see `LICENSE`).
- Our report: [Creative Commons Attribution 4.0 (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
- TRAK itself is released by its authors under the MIT License (Copyright (c) 2023 Madry Lab). The patch in `patches/` modifies one line of their code and remains under their license.
