# SRK-Crystallizer v2.1 (Industrial Engine)

Ultra-lightweight, deterministic Model Context Protocol (MCP) server engineered for autonomous coding agents. Provides surgical in-memory AST code patching, zero memory footprint, zero bytecode distribution (native C engine), and hardware-grade atomic rollback.

---

## 1. EXECUTIVE SUMMARY

**SRK-Crystallizer v2.1** addresses the primary economic and physical bottlenecks of modern coding agents (Claude, OpenCode, Codex, Gemini):
1. **Elimination of Full-File Rewrites:** Replaces repetitive full-file dumps with atomic surgical micro-patches (`srk_patch`).
2. **KV-Cache Preservation:** Compact AST contract mapping (`srk_map`) and targeted symbol rehydration (`srk_read`) slash input context tokens by more than half.
3. **Hardware-Grade Safety & Inviolability:** In-memory AST pre-validation before disk writes, masked secrets overwrite prevention, strict SHA-256 desynchronization guards (Stale SHA), and atomic filesystem pointer replacement (`os.replace`).
4. **Hardened Native Binary Distribution:** x86-64 standalone executable transpiled to native machine code via Nuitka C + Link-Time Optimization (LTO), completely stripped of Python bytecode and immune to decompilers / Reverse Engineering Agents (Anti-REA).

---

## 2. CERTIFIED BENCHMARKS & MEASURED METRICS [MEASURED]

### A/B Comparative Benchmark (Real 814-line System File)
Measured using the official `cl100k_base` tokenizer via `tiktoken`:

| Consumption Metric | Standard Workflow | SRK-Crystallizer v2.1 | Measured Reduction [MEASURED] |
| :--- | :---: | :---: | :---: |
| **Input Tokens (weight x1.25)** | 9,268 tokens | 4,441 tokens | **-52.08%** |
| **Output Tokens (weight x5.0)** | 9,283 tokens | 15 tokens | **-99.84%** |
| **Total Raw Tokens** | 18,551 tokens | 4,456 tokens | **-75.98%** |
| **Weighted Quota Units** | **58,000.00** | **5,626.25** | **-90.30%** |

$$\text{Official Quota Formula} = (\text{Input Tokens} \times 1.25) + (\text{Output Tokens} \times 5.0)$$

### Deterministic Multi-Turn Session (10 Sequential Code Modifications)
- **Cumulative Input Tokens:** 8,992 vs 93,175 (**-90.35%**)
- **Cumulative Output Tokens:** 110 vs 93,285 (**-99.88%**)
- **Cumulative Quota Savings (10 turns):** **-97.98%**

### 4-Stage Industrial Hardening Suite
1. **Stage 1 (Formats & Encodings):** Native support for mixed CRLF/LF, Arabic script (`سيرفر`), accented characters, and emojis. Surgical 1-line diff with zero parasite diff.
2. **Stage 2 (Concurrency & Race Conditions):** 2 simultaneous clients on identical initial hash: exactly 1 commit (`OK`), 1 instant rejection (`ERR_STALE_SHA`), 0 corruption.
3. **Stage 3 (AST Stress & Deep Recursion):** Validated on 2,704 lines with deep asynchronous structures without recursion limit or memory leaks.
4. **Stage 4 (Local CPU Micro-Latency over 50 iterations):**
   - `srk_map`: Median = **74.97 ms** (Mean = 78.33 ms)
   - `srk_read`: Median = **76.22 ms** (Mean = 81.32 ms)
   - `srk_patch`: Median = **166.74 ms** (Mean = 179.10 ms)

---

## 3. MCP CLIENT INTEGRATION GUIDE

The server communicates using the standard Model Context Protocol (MCP) over `stdio` via JSON-RPC.

### Claude Desktop Integration (`claude_desktop_config.json`)
```json
{
  "mcpServers": {
    "srk-crystallizer": {
      "command": "bin/srk-crystallizer.exe"
    }
  }
}
```

### OpenCode Integration (`opencode.json`)
```json
{
  "mcp": {
    "srk-crystallizer": {
      "type": "local",
      "command": [
        "bin/srk-crystallizer.exe"
      ],
      "enabled": true
    }
  }
}
```

---

## 4. OFFICIAL BINARY INTEGRITY & VERIFICATION

To verify binary authenticity and integrity:

- **Target File:** `bin/srk-crystallizer.exe`
- **Format:** Standalone native x86-64 binary (`onefile`, LTO, Stripped)
- **Size:** 23,931,904 bytes (22.82 MB)
- **Official SHA-256 Hash:**
  ```text
  89787a6dc5954054f3e037dd1b37a719f4c0499fd70da0278d82e626dbe87294
  ```

---

## 5. INTELLECTUAL PROPERTY & LICENSE

## License & Rights
This project is distributed under the Proprietary Binary Distribution License.  
Free to use and integrate across personal, academic, and enterprise MCP clients.  
Copyright © 2026 **PapyTechnologies**. All rights reserved.
