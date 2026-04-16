# Microscaling (MX) Quantization Benchmark Study
**Note:** This benchmark is still in progress. Results are being actively collected and validated.

This benchmark evaluates **MXINT** quantization formats against standard per-tensor INT quantization on vision-language models. MXINT uses block-wise scaling (groups of weights share a scaling factor), while standard INT applies a single scale across entire tensors. We test on VQA v2 and TextVQA datasets across five VLMs ranging from 1B to 8B parameters.

**Key technical points:**
- **MXINT formats**: INT8/4/2 with block-wise scaling (32-element blocks primary, 128-element secondary)
- **Standard INT**: Per-tensor scaling (single scale factor per weight tensor)
- **BF16 baseline**: Native precision for each model
- Models tested: SmolVLM2-2.2B, Phi-4-multimodal, Qwen3-VL-2B, Gemma3-4B, InternVL-3.5-1B, Eagle2.5-8B

---

## Critical Finding: MXINT4 Stability vs. INT4 Collapse

**Standard per-tensor INT4 causes catastrophic model failure** (0.00% accuracy) across all tested VLMs, while **MXINT4 with block-wise scaling maintains 85-97% of BF16 performance**. 

This divergence stems from quantization granularity: per-tensor INT4 forces extreme weight distributions into 16 discrete levels using a single global scale, destroying within-tensor variance. Block-wise scaling in MXINT4 preserves local weight structure by applying independent scales per 32-element block, preventing information collapse in weight-sensitive transformer layers. INT8 remains viable in both schemes due to 256 quantization bins providing sufficient resolution even with coarse scaling.

---

## Model Benchmark Results
| Model         | Precision | VQA  | TextVQA |
|---------------|----------|------|---------|
| SmolVLM2-2.2b | BF16     | 62.77 | 64.5    |
| Phi-4-multimodal-instruct | BF16     | 71.57 | 63.03    |
| Qwen3-VL-2B | BF16     | 78.59 | 79.84    |
| Gemma3-4B | BF16     | 48.83 | 59.19    |
| InternVL-3.5-1B | BF16     | 72.90 | 68.30    |
| Molmo-7B-D | BF16     | 59.07 | 56.63    |
| Eagle-2.5-8B | BF16     | remaining | remaining    |

### Quantized Results
| Model         | Precision | Block Size | VQA   | TextVQA |
|---------------|----------|------------|-------|---------|
| SmolVLM2-2.2b | MXINT8   | 32         | 63.17 | 64.19   |
|               |          | 128        | 62.11 | 64.33   |
| SmolVLM2-2.2b | MXINT4   | 32         | 73.43 | 59.3    |
|               |          | 128        | 73.08 | 57.29   |
| SmolVLM2-2.2b | MXINT2   | 32         | 0.00     | 0.00       |
|               |          | 128        | 0.00     | 0.00       |
| SmolVLM2-2.2b | INT8   | - | 54.63 | 60.81    |
| SmolVLM2-2.2b | INT4   | -    | 0.00   | 0.00  |
| SmolVLM2-2.2b | INT2   | -         | 0.00     | 0.00       |
| Phi-4-multimodal-instruct | MXINT8   | 32         | 71.57 | 62.93   |
|               |          | 128        | - | -   |
| Phi-4-multimodal-instruct | MXINT4   | 32         | 67.64 | 59.06    |
|               |          | 128        | - | -   |
| Phi-4-multimodal-instruct | MXINT2   | 32         | 0.00     | 0.00       |
|               |          | 128        | -     | -       |
| Phi-4-multimodal-instruct | INT8   | - | 70.33 | 61.70    |
| Phi-4-multimodal-instruct | INT4   | -    | 0.02   | 0.00  |
| Phi-4-multimodal-instruct | INT2   | -         | 0.00     | 0.00       |
| Qwen3-VL-2B | MXINT8   | 32         | 78.27 | 79.75   |
|               |          | 128        | - | -   |
| Qwen3-VL-2B | MXINT4   | 32         | 76.47 | 75.50    |
|               |          | 128        | - | -   |
| Qwen3-VL-2B | MXINT2   | 32         | -     | -       |
|               |          | 128        | 0.00     | 0.00       |
| Qwen3-VL-2B | INT8   | - | 78.37 | 79.25    |
| Qwen3-VL-2B | INT4   | -    | 0.00   | 0.00  |
| Qwen3-VL-2B | INT2   | -         | 0.00     | 0.00       |
| Gemma3-4B | MXINT8   | 32         | 48.49 | 59.41   |
|               |          | 128        | - | -   |
| Gemma3-4B | MXINT4   | 32         | 47.01 | 58.52    |
|               |          | 128        | - | -   |
| Gemma3-4B | MXINT2   | 32         | 0.00     | 0.00       |
|               |          | 128        | -     | -       |
| Gemma3-4B | INT8   | - | 44.91 | 57.09    |
| Gemma3-4B | INT4   | -    | 0.00   | 0.00  |
| Gemma3-4B | INT2   | -         | 0.00     | 0.00       |
| InternVL-3.5-1B | MXINT8   | 32         | 72.79 | 68.35   |
|               |          | 128        | - | -   |
| InternVL-3.5-1B | MXINT4   | 32         | 68.17 | 64.73    |
|               |          | 128        | - | -   |
| InternVL-3.5-1B | MXINT2   | 32         | 0.00     | 0.00       |
|               |          | 128        | -     | -       |
| InternVL-3.5-1B | INT8   | - | 72.08 | 67.17    |
| InternVL-3.5-1B | INT4   | -    | 0.00   | 0.00  |
| InternVL-3.5-1B | INT2   | -         | 0.07     | 0.41       |
| Molmo-7B-D | MXINT8   | 32         | 59.00 | 56.37   |
|               |          | 128        | - | -   |
| Molmo-7B-D | MXINT4   | 32         | 56.29 | 52.92    |
|               |          | 128        | - | -   |
| Molmo-7B-D | MXINT2   | 32         | 0.00     | 0.00       |
|               |          | 128        | -     | -       |
| Molmo-7B-D | INT8   | - | 58.97 | 57.29    |
| Molmo-7B-D | INT4   | -    | 0.47   | 0.05  |
| Molmo-7B-D | INT2   | -         | 0.07     | 0.41       |
| Eagle-2.5-8B | MXINT8   | 32         | 82.41 | 82.75   |
|               |          | 128        | - | -   |
| Eagle-2.5-8B | MXINT4   | 32         | 81.31 | 81.25    |
|               |          | 128        | - | -   |


---
