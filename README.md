# Reproducing HAWQ-V3: Hessian-Based Mixed-Precision Quantization

A reproduction of [HAWQ-V3](https://arxiv.org/abs/2011.10680) on CIFAR-10 with ResNet-18.

Uniform 4-bit quantization usually costs a lot of accuracy, because some layers are far more sensitive to quantization noise than others. HAWQ-V3 measures each layer's sensitivity from its Hessian and keeps the sensitive layers at higher precision while dropping the robust ones lower.

## What we did

- Estimated each layer's sensitivity with a gradient-based Hessian trace approximation
- Built a cost model from parameter counts and bit operations
- Used a greedy search to assign 4-bit or 8-bit precision to each layer under a model-size budget

## Result

Targeting a 41% smaller model cost only 0.95 points of accuracy (78.70% to 77.75%). The full pipeline runs in about 15 minutes on a single GPU.

## Report

[HAWQ-V3_Reproduction_Report.pdf](HAWQ-V3_Reproduction_Report.pdf)
