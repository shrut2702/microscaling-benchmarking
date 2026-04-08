## Model Benchmark Results

| Model         | Precision | VQA  | TextVQA |
|---------------|----------|------|---------|
| SmolVLM2-2.2b | BF16     | 62.77 | 64.5    |
| Phi-4-multimodal-instruct | BF16     | 71.57 | 63.03    |
| Qwen3-VL-2B | BF16     | 78.59 | 79.84    |
| Gemma3-4B | BF16     | 48.83 | 59.19    |
| InternVL-3.5-1B | BF16     | 72.90 | 68.30    |

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


---
