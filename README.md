<div align="center">

# Boundary-Guided Colorectal Polyp Segmentation

### Lightweight Boundary-Guided Colorectal Polyp Segmentation with Size-Aware Training

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.x-EE4C2C?logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Dataset](https://img.shields.io/badge/Dataset-Kvasir--SEG-7B2CBF)](https://datasets.simula.no/kvasir-seg/)
[![Conference](https://img.shields.io/badge/INCISCOS_V_2026-Accepted-2ea44f)](https://inciscos.ute.edu.ec/)

</div>

## Overview

This project studies lightweight segmentation of colorectal polyps in colonoscopy images. The method uses an EfficientNet-B0 encoder, multi-scale context, and a boundary prediction branch whose attention signal guides decoder features. Size-aware sampling increases exposure to underrepresented small and very large polyps.

The paper, **“Lightweight Boundary-Guided Colorectal Polyp Segmentation with Size-Aware Training”** (Paper 65), was accepted for presentation at INCISCOS V 2026 in Quito, Ecuador (November 17–19, 2026).

> The submitted notebook uses the implementation name **LiteTC-PolypNet-B0-SWA**; the manuscript refers to the proposed approach as **BG-PolypNet-SWA**.

## Method at a glance

- **Dataset:** Kvasir-SEG, 1,000 image-mask pairs
- **Partition:** 800 training, 100 validation, and 100 held-out test images; mask-area-stratified, seed 42
- **Input:** acquisition-border crop followed by resize to 352 × 352
- **Boundary guidance:** one supervised boundary map is reused as a residual attention gate in the decoder
- **Training:** size-aware sampling, composite segmentation and boundary losses, and stochastic weight averaging
- **Inference selection:** validation-selected threshold and horizontal-flip TTA; settings frozen before final test evaluation

## Final test results

The final single-model checkpoint was evaluated on the 100-image held-out test partition.

| Metric | Result |
|---|---:|
| Dice | **0.9213** |
| IoU | **0.8731** |
| Precision | **0.9281** |
| Recall | **0.9400** |
| Parameters | **4.804M** |
| MACs at 352 × 352 | **1.844G** |
| Throughput | **43.7 FPS** |

The paper reports the final Stage 2 + SWA configuration. Literature comparisons are reported as published by their respective authors and were not reproduced under a common training protocol.

## Repository contents

```text
litetc-polypnet-b0/
├── notebooks/litetc_polypnet_b0.ipynb
├── requirements.txt
└── README.md
```

The notebook output was cleared for the public release. Run it in sequence to regenerate the training logs, checkpoints, figures, and evaluation tables. The final accepted-paper analysis also includes validation-only selection and test-set reporting.

## Reproducibility and scope

Results are from one fixed Kvasir-SEG split and seed. The evaluation does not establish cross-dataset generalization or clinical readiness. The code is for research and education and is not a clinically validated polyp-detection system.

## Contact

**Protik Biswas** · [GitHub](https://github.com/pkhunter47) · [LinkedIn](https://www.linkedin.com/in/protik-biswas-83001827b/) · [Email](mailto:protikbiswas3099@gmail.com)
