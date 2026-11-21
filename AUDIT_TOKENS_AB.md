# COMPARATIVE A/B AUDIT: SRK-CRYSTALLIZER v2.1 vs STANDARD WORKFLOW

Evaluation Date: November 21, 2026  
Tokenizer: Official `cl100k_base` via `tiktoken`  
Target File: Real Python system file of 814 lines (36,547 characters)  
Identical Task: Target symbol identification (`refus_ecriture`), surgical extraction, and safety guard insertion with AST validation and runtime unit verification.

---

## 1. OFFICIAL BENCHMARK METRICS COMPARISON

| METRIC / PARAMETER | CONDITION A (STANDARD) | CONDITION B (SRK-CRYSTALLIZER v2.1) | MEASURED REDUCTION [MEASURED] |
| :--- | :---: | :---: | :---: |
| **Context Injected Bytes (In)** | 37,599 bytes | 14,789 bytes | **-60.67%** |
| **Agent Emitted Bytes (Out)** | 36,847 bytes | 61 bytes | **-99.83%** |
| **Input Tokens (weight x1.25)** | 9,268 tokens | 4,441 tokens | **-52.08%** |
| **Output Tokens (weight x5.0)** | 9,283 tokens | 15 tokens | **-99.84%** |
| **Total Raw Tokens** | 18,551 tokens | 4,456 tokens | **-75.98%** |
| **Weighted Quota Units** | **58,000.00** | **5,626.25** | **-90.30%** |

Official Weighted Quota Units Formula:
$$\text{Quota} = (\text{Input Tokens} \times 1.25) + (\text{Output Tokens} \times 5.0)$$

---

## 2. PHYSICAL EFFICIENCY ANALYSIS

1. **Surgical Output (Weight x5.0):**
   - Standard workflow forces the agent to rewrite the entire file (9,283 tokens emitted).
   - With `srk_patch`, the agent emits only the modified code lines (15 tokens emitted), delivering a **-99.84%** reduction on the costliest token category.

2. **Contract-Based Input (Weight x1.25):**
   - Standard workflow consumes the entire raw file into context (9,268 tokens).
   - With `srk_map` + `srk_read`, the agent digests the compact signature contract and only the targeted symbol body (4,441 tokens), delivering a **-52.08%** reduction.

3. **Validation & Resilience:**
   - Zero syntax regressions (in-memory AST compilation passed with 0 `SyntaxError`).
   - Logical integrity verified through isolated runtime execution.
