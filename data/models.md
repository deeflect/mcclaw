# McClaw Model Database

This file contains the public LLM compatibility data used by McClaw.

## Device Configurations

| Configuration | Chip | RAM | Usable RAM | Price |
|---------------|------|-----|------------|-------|
| M4 16GB | M4 | 16 GB | ~12 GB | $599 |
| M4 24GB | M4 | 24 GB | ~18 GB | $799 |
| M4 32GB | M4 | 32 GB | ~26 GB | $999 |
| M4 Pro 24GB | M4 Pro | 24 GB | ~18 GB | $1,399 |
| M4 Pro 48GB | M4 Pro | 48 GB | ~40 GB | $1,999 |
| M4 Pro 64GB | M4 Pro | 64 GB | ~54 GB | $2,199 |

**Note:** "Usable RAM" accounts for macOS overhead (~4-6GB depending on background apps).

---

## Models by Category

### 🤖 Agent / General Purpose

| Model | Parameters | q4_k_m RAM | q8_0 RAM | Context | Best For |
|-------|------------|------------|----------|---------|----------|
| Llama 3.1 8B | 8B | 6.5 GB | 10 GB | 128K | Versatile chat, reasoning |
| Llama 3.1 70B | 70B | 42 GB | 75 GB | 128K | Complex reasoning (needs 64GB) |
| Mistral 7B | 7B | 5 GB | 8.5 GB | 32K | Fast general purpose |
| Mixtral 8x7B | 47B | 28 GB | 50 GB | 32K | MoE, good balance |

### 💻 Code

| Model | Parameters | q4_k_m RAM | q8_0 RAM | Context | Best For |
|-------|------------|------------|----------|---------|----------|
| Qwen 2.5 Coder 14B | 14B | 10.5 GB | 16 GB | 128K | Function calling, tools |
| DeepSeek Coder 33B | 33B | 22 GB | 38 GB | 16K | Complex codebases |
| CodeLlama 34B | 34B | 22 GB | 40 GB | 16K | Code completion |
| StarCoder2 15B | 15B | 11 GB | 18 GB | 16K | Multi-language coding |

### 🧠 Reasoning

| Model | Parameters | q4_k_m RAM | q8_0 RAM | Context | Best For |
|-------|------------|------------|----------|---------|----------|
| DeepSeek R1 32B | 32B | 22 GB | 38 GB | 128K | Deep reasoning, CoT |
| Phi-3 Medium 14B | 14B | 9.5 GB | 16 GB | 128K | Efficient reasoning |
| Qwen 2.5 72B | 72B | 45 GB | 80 GB | 32K | Frontier-level (needs 64GB) |

### 👁️ Vision / Multimodal

| Model | Parameters | q4_k_m RAM | q8_0 RAM | Context | Best For |
|-------|------------|------------|----------|---------|----------|
| LLaVA 7B | 7B | 6 GB | 9.5 GB | 4K | Image understanding |
| LLaVA 13B | 13B | 9 GB | 15 GB | 4K | Better image analysis |
| Qwen-VL 7B | 7B | 6 GB | 10 GB | 8K | Vision + Chinese |

### ⚡ Small & Fast

| Model | Parameters | q4_k_m RAM | q8_0 RAM | Context | Best For |
|-------|------------|------------|----------|---------|----------|
| Phi-3 Mini 3.8B | 3.8B | 3 GB | 5 GB | 128K | Ultra-fast responses |
| TinyLlama 1.1B | 1.1B | 1.5 GB | 2.5 GB | 2K | Edge/embedded use |
| Gemma 2B | 2B | 2 GB | 4 GB | 8K | Lightweight tasks |

---

## Quantization Guide

| Quantization | Quality | Size | Speed | Recommended Use |
|--------------|---------|------|-------|-----------------|
| **q4_k_m** | 95% | 50% | Fast | ✅ Default choice |
| **q5_k_m** | 97% | 60% | Good | Quality/size balance |
| **q8_0** | 99% | 100% | Slower | When quality matters |
| **fp16** | 100% | 200% | Slowest | Benchmarking only |

### What does this mean?

- **q4_k_m**: 4-bit quantization with k-means clustering. Best balance for most users.
- **q8_0**: 8-bit quantization. Noticeably better for complex reasoning.
- **fp16**: Full 16-bit precision. Only use if you have RAM to spare.

---

## RAM Recommendations by Use Case

### Casual Chat (16GB Mac)
- ✅ Llama 3.1 8B (q4_k_m)
- ✅ Mistral 7B (q4_k_m)
- ✅ Phi-3 Mini 3.8B

### Coding Assistant (24-32GB Mac)
- ✅ Qwen 2.5 Coder 14B (q4_k_m)
- ✅ DeepSeek Coder 6.7B (q8_0)
- ✅ CodeLlama 13B (q4_k_m)

### Power User (48-64GB Mac)
- ✅ Llama 3.1 70B (q4_k_m)
- ✅ Mixtral 8x7B (q4_k_m)
- ✅ DeepSeek R1 32B (q8_0)
- ✅ Qwen 2.5 72B (q4_k_m)

---

## Benchmark Sources

- **MMLU**: Measuring Massive Multitask Language Understanding
- **HumanEval**: Code generation benchmark (0-shot pass@1)
- **GPQA**: Graduate-level reasoning questions
- **MT-Bench**: Multi-turn conversation quality

All benchmarks sourced from:
- Official model papers
- Open LLM Leaderboard
- Ollama model cards
- Personal testing on M4 Mac Mini 32GB

---

## Ollama Commands

```bash
# Install Ollama
brew install ollama

# Start the server
ollama serve

# Pull a model
ollama pull llama3.1:8b          # Default quantization
ollama pull llama3.1:8b-q8_0     # Higher quality

# Run interactively
ollama run llama3.1:8b

# List installed models
ollama list

# Remove a model
ollama rm llama3.1:8b
```

---

*Data last updated: February 2026*
