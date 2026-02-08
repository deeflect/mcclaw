<p align="center">
  <img src="assets/favicon.png" width="80" alt="McClaw logo" />
</p>

<h1 align="center">McClaw</h1>

<p align="center">
  find the right local LLM for your mac<br/>
  <em>stop guessing if that 70B model will fit</em>
</p>

<p align="center">
  <a href="https://mcclaw.it.com">live site</a> •
  <a href="https://x.com/deeflectcom">twitter</a>
</p>

---

![og image](assets/og-image.jpg)

## the problem

running local LLMs on mac is confusing:

- "will this model fit in 32GB RAM?"
- "q4_k_m vs q8_0... what?"
- "which one is good for coding?"

most people download something too big, it crashes, they give up and go back to paying for API calls.

## the solution

a 3-step wizard:

1. pick your mac (M4 / M4 Pro, RAM size)
2. pick your experience level  
3. see exactly which models fit

no guessing. no trial and error.

![setup wizard](screenshots/setup-wizard.jpg)

## tech

| what | why |
|------|-----|
| **React 18 + TS** | stable, nothing fancy needed |
| **Framer Motion** | smooth wizard transitions |
| **Tailwind** | fast iteration |
| **Convex** | just for cloud model price comparison |
| **Vercel** | free tier |

### why no backend?

all the model data is static — compiled into the frontend. benefits:

- instant filtering (no API calls)
- works offline after first load
- updating = just redeploy

## the data

50+ models with variants. sample:

| model | params | q4_k_m RAM | category |
|-------|--------|------------|----------|
| Qwen 2.5 Coder 14B | 14B | 10.5 GB | coding |
| Llama 3.1 8B | 8B | 6.5 GB | general |
| DeepSeek R1 32B | 32B | 22 GB | reasoning |
| LLaVA 7B | 7B | 6 GB | vision |

full model database in [data/models.md](data/models.md)

### device configs

```typescript
devices = {
  "m4-16":    { usableRam: 12 },  // ~4GB for macOS
  "m4-24":    { usableRam: 18 },
  "m4-32":    { usableRam: 26 },
  "m4pro-48": { usableRam: 40 },
  "m4pro-64": { usableRam: 54 },
}
```

## how matching works

```typescript
// pseudocode
models
  .flatMap(model => model.variants)
  .filter(variant => variant.ramGb <= device.usableRam)
  .sort(by benchmark scores, then popularity)
```

![results](screenshots/results.jpg)

## design

went apple-inspired on purpose:
- centered content
- minimal chrome
- big tappable buttons
- progress dots

feels familiar to mac users, builds trust.

### progressive disclosure

beginners get "Top Picks" — curated recommendations.
experts get the full table with all quantizations and benchmarks.

## quantization quick ref

| quant | quality | size | use case |
|-------|---------|------|----------|
| **q4_k_m** | 95% | 50% | default choice |
| **q8_0** | 99% | 100% | when quality matters |
| **fp16** | 100% | 200% | benchmarking only |

## maybe later

- [ ] MacBook support (not just Mac Mini)
- [ ] user-submitted performance reports
- [ ] direct Ollama integration

---

built by [@deeflectcom](https://x.com/deeflectcom) for the [OpenClaw](https://openclaw.ai) community

model data from Ollama, official papers, Open LLM Leaderboard, and personal testing on M4 Mac Mini 32GB
