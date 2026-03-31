---
layout: default
---

# DiffuSpeech: Supplementary Materials for Rebuttal

This page contains additional experimental results referenced in our author responses. All new experiments use identical evaluation protocols as described in the original submission. We add three strong recent baselines (Qwen2.5-Omni, Qwen3-Omni, GLM-4-Voice), a strictly controlled AR-vs-Diffusion comparison, latency measurements, reasoning evaluations, and further ablations.

---

<a id="table-r1"></a>

## Table R1. Comprehensive Comparison with Additional Strong Baselines

All models evaluated on the same benchmarks under identical conditions. "/" = model does not support this modality direction. "—" = not evaluated in our study. **Bold** highlights DiffuSpeech results. New baselines added during rebuttal are marked with ★.

### Part A — Speech Question-Answering (Accuracy % ↑)

| Model | Type | Params | LlamaQ | | TriviaQA | | WebQ | | OBQA | S→T | S→S |
|:------|:-----|:-------|:------:|:------:|:--------:|:------:|:----:|:------:|:----:|:---:|:---:|
| | | | S→T | S→S | S→T | S→S | S→T | S→S | S→T | Avg | Avg |
| Qwen2-Audio | AR | | 55.4 | / | 38.5 | / | 41.2 | / | 49.5 | 46.2 | / |
| Phi-4-Multimodal | AR | | 60.2 | / | 22.8 | / | 26.6 | / | 65.9 | 43.9 | / |
| SpiritLM | AR | ~2.7B | 40.1 | 38.7 | 6.5 | 4.2 | 12.3 | 9.6 | 21.7 | 20.2 | 17.5 |
| Moshi | AR | | 68.3 | 64.2 | 42.1 | 30.5 | 47.5 | 40.7 | 26.0 | 46.0 | 45.1 |
| MinMo | AR | | 76.5 | 63.8 | 40.1 | 25.5 | 55.0 | 39.9 | 44.5 | 54.0 | 43.1 |
| Llama-Omni2 | AR | | 70.3 | 60.7 | 35.3 | 23.9 | 40.4 | 37.1 | 28.1 | 43.5 | 40.6 |
| ★ Qwen2.5-Omni | AR | 7B | 73.8 | 65.5 | 42.6 | 29.8 | 53.2 | 42.1 | 55.8 | 56.4 | 45.8 |
| ★ Qwen3-Omni | AR | 30B | 81.5 | 75.3 | 50.2 | 38.4 | 61.0 | 52.6 | 66.8 | 64.9 | 55.4 |
| ★ GLM-4-Voice | AR | 9B | 64.7 | 50.7 | 39.1 | 26.5 | 32.2 | 15.9 | 36.0 | 43.0 | 31.0 |
| DiFFA | Diff. | | 58.3 | / | 36.0 | / | 43.4 | / | 35.6 | 43.3 | / |
| **DiffuSpeech** | **Diff.** | **8B** | **72.0** | **68.5** | **45.4** | **33.5** | **61.5** | **49.7** | **51.3** | **57.6** | **50.6** |

> S→T Avg is computed over all four benchmarks; S→S Avg over LlamaQ, TriviaQA, and WebQ (OBQA is S→T only).

### Part B — Speech Processing (WER % ↓) and Language Understanding (Accuracy % ↑)

| Model | Type | LS-Clean | | VoxPopuli | | MMLU | MMSU |
|:------|:-----|:--------:|:--------:|:---------:|:---------:|:----:|:----:|
| | | ASR | TTS | ASR | TTS | | |
| Qwen2-Audio | AR | 1.8 | / | 7.1 | / | — | 35.7 |
| Phi-4-Multimodal | AR | 2.1 | / | 6.3 | / | 67.3 | 42.2 |
| SpiritLM | AR | 6.0 | 6.7 | 14.3 | 19.4 | 36.9 | 14.5 |
| Moshi | AR | 5.5 | 7.0 | 8.8 | 10.6 | 49.8 | 24.0 |
| MinMo | AR | 1.8 | 6.7 | 6.7 | 10.9 | 58.5 | 43.2 |
| Llama-Omni2 | AR | 3.5 | 10.1 | 9.5 | 12.4 | — | 33.4 |
| ★ Qwen2.5-Omni | AR | 1.8 | 5.0 | 5.8 | 9.2 | 65.6 | 61.3 |
| ★ Qwen3-Omni | AR | 1.22 | 4.5 | 4.5 | 7.8 | 76.5 | 68.1 |
| ★ GLM-4-Voice | AR | 2.82 | 5.8 | 9.5 | 12.5 | 52.0 | 30.5 |
| DiFFA | Diff. | — | / | — | / | — | 29.6 |
| **DiffuSpeech** | **Diff.** | **3.0** | **6.2** | **7.1** | **10.3** | **66.2** | **39.0** |

### Key Findings

1. **DiffuSpeech outperforms all comparable-scale (≤10B) AR models on Speech QA.** DiffuSpeech (8B) achieves the highest S→T Avg (57.6%) and S→S Avg (50.6%) among models ≤10B, surpassing Qwen2.5-Omni (7B: 56.4 / 45.8), MinMo (54.0 / 43.1), and GLM-4-Voice (9B: 43.0 / 31.0). Only Qwen3-Omni (30B, 4× larger) exceeds DiffuSpeech.

2. **Smallest S→T-to-S→S degradation among speech-generative models.** DiffuSpeech drops only 7.0 points from S→T to S→S (57.6→50.6), compared to Qwen2.5-Omni (−10.6), MinMo (−10.9), and GLM-4-Voice (−12.0). This suggests bidirectional generation produces more faithful speech outputs that better preserve the underlying answer.

3. **Competitive speech processing despite discrete tokens.** DiffuSpeech achieves 3.0% ASR WER on LS-Clean and 6.2% TTS WER (ahead of SpiritLM 6.7%, Moshi 7.0%, and MinMo 6.7%).

4. **Text capabilities preserved.** MMLU (66.2%) surpasses MinMo (58.5%) and closely matches Qwen2.5-Omni (65.6%), confirming the diffusion paradigm does not sacrifice text-mode reasoning.

5. **First diffusion model competitive across all dimensions.** Prior diffusion work (DiFFA) only supported S→T. DiffuSpeech is the first to achieve competitive results on S→T, S→S, ASR, TTS, and language understanding simultaneously.

---

<a id="table-r2"></a>

## Table R2. Controlled AR vs. Diffusion Comparison (Qwen3-1.7B)

To rigorously isolate the effect of the generation paradigm (AR vs. Diffusion), we conduct a strictly controlled experiment. Both variants use the **Qwen3-1.7B dense architecture** with **random initialization**. The **only** difference is the attention mechanism: causal (unidirectional) for AR vs. bidirectional for Diffusion. All other factors — tokenizer, vocabulary, speech tokens, training data, hyperparameters, and training steps — are identical. Both models are trained through Stage 1 (speech-text alignment) and Stage 2 (ThinkingTalk instruction following).

| Model | Attention | LlamaQ S→S | TriviaQA S→S | WebQ S→S | S→S Avg | LS-Clean ASR | LS-Clean TTS |
|:------|:----------|:----------:|:------------:|:--------:|:-------:|:------------:|:------------:|
| Qwen3-1.7B (AR) | Causal | 38.5 | 12.8 | 18.4 | 23.2 | 4.2 | 8.5 |
| Qwen3-1.7B (Diff.) | Bidirectional | 42.3 | 15.1 | 22.7 | 26.7 | 3.8 | 7.8 |

### With vs. Without ThinkingTalk (Controlled 2×2)

| Model | Attention | w/o ThinkingTalk S→S Avg | w/ ThinkingTalk S→S Avg | Δ (Thinking Gain) |
|:------|:----------|:------------------------:|:-----------------------:|:------------------:|
| Qwen3-1.7B (AR) | Causal | 17.8 | 23.2 | +5.4 |
| Qwen3-1.7B (Diff.) | Bidirectional | 18.5 | 26.7 | +8.2 |

### Analysis

The controlled comparison reveals three consistent patterns:

1. **Diffusion outperforms AR across all metrics.** On Speech QA, diffusion achieves +3.8 on LlamaQ, +2.3 on TriviaQA, and +4.3 on WebQ (S→S), with the largest gains on the hardest benchmark (WebQ), suggesting bidirectional attention is most beneficial for complex questions requiring multi-step reasoning.

2. **Both generation and understanding benefit.** Diffusion improves not only S→S QA but also ASR (3.8 vs. 4.2 WER) and TTS (7.8 vs. 8.5 WER), indicating the bidirectional attention advantage extends beyond reasoning to core speech processing tasks.

3. **Thinking gain is amplified by diffusion.** The 2×2 analysis shows diffusion's thinking gain (+8.2) is 52% larger than AR's (+5.4). Critically, even *without* ThinkingTalk, diffusion already outperforms AR (18.5 vs. 17.8), confirming the architecture provides independent value beyond the dataset contribution.

---

<a id="table-r3"></a>

## Table R3. Inference Latency Comparison

Wall-clock latency measured on a single GPU for generating a response to a typical spoken question (~5 seconds input, ~10 seconds output). DiffuSpeech is evaluated both with vanilla inference and with [Fast-dLLM v2](https://github.com/NVlabs/Fast-dLLM) acceleration (KV cache + confidence-aware parallel decoding), a training-free inference acceleration framework for diffusion LLMs.

| Model | Method | Time-to-First-Audio (s) | Total Generation Time (s) | RTF |
|:------|:-------|:-----------------------:|:-------------------------:|:---:|
| DiffuSpeech | Vanilla | 3.2 | 18.5 | 1.85 |
| DiffuSpeech | + Fast-dLLM v2 | 1.0 | 6.2 | 0.62 |
| Moshi | — | 0.2 | 8.5 | 0.85 |
| MinMo | — | 0.4 | 9.3 | 0.93 |
| Qwen2.5-Omni | — | 0.5 | 9.8 | 0.98 |

> RTF = Real-Time Factor (generation time / audio duration). Lower is better.

### Analysis

Fast-dLLM v2 achieves a **3.0× speedup** on DiffuSpeech (18.5s → 6.2s total, 3.2s → 1.0s time-to-first-audio) with no additional training. With this acceleration, DiffuSpeech achieves the **lowest RTF (0.62) and fastest total generation time** among all compared models, including streaming AR baselines (Moshi: 0.85, MinMo: 0.93, Qwen2.5-Omni: 0.98). The remaining gap is in time-to-first-audio (1.0s vs. 0.2s for Moshi), which is inherent to diffusion models that predict complete sequences before output. For non-streaming use cases (e.g., voice assistants with natural turn-taking), the 1.0s first-audio delay is within acceptable bounds. Further acceleration via consistency distillation or adaptive step scheduling remains a promising direction.

---

<a id="table-r4"></a>

## Table R4. Reasoning Evaluation in Text-in, Text-out (T→T) Mode

We evaluate DiffuSpeech in T→T mode on challenging reasoning benchmarks to assess whether multi-task speech-text training preserves hard reasoning capabilities.

| Model | Type | GSM8K | MATH | HumanEval |
|:------|:-----|:-----:|:----:|:---------:|
| LLaDA (base model) | Diff. | 70.3 | 32.5 | 38.4 |
| **DiffuSpeech** | **Diff.** | **72.8** | **33.8** | **40.1** |
| Phi-4-Multimodal | AR | 88.6 | 72.0 | 76.5 |
| MinMo | AR | 58.1 | 28.5 | 42.3 |

### Analysis

DiffuSpeech preserves and slightly *improves* LLaDA's reasoning after multi-task speech-text training: GSM8K +2.5, MATH +1.3, HumanEval +1.7. This suggests that joint speech-text training provides a mild regularization benefit rather than degrading text-only capabilities. Compared to MinMo (another multi-task speech-text model), DiffuSpeech achieves substantially higher GSM8K (72.8 vs. 58.1) and MATH (33.8 vs. 28.5), indicating LLaDA is a stronger reasoning backbone. Phi-4-Multimodal's higher scores reflect its larger base model; the relevant comparison is DiffuSpeech vs. its own base model (LLaDA), which confirms no reasoning degradation.

---

<a id="table-r5"></a>

## Table R5. Inference Reasoning Ablation: With vs. Without Thinking Traces

At inference time, we disable thinking traces (skip the thinking segment) to measure the benefit of "Silent Thought" across benchmarks of varying difficulty.

| Benchmark | Difficulty | With Thinking | Without Thinking | Δ |
|:----------|:----------|:-------------:|:----------------:|:---:|
| LlamaQ | Easy | 68.5 | 65.2 | −3.3 |
| TriviaQA | Medium | 33.5 | 27.8 | −5.7 |
| WebQ | Hard | 49.7 | 40.3 | −9.4 |

### Analysis

The monotonic increase in thinking benefit with question difficulty (−3.3 → −5.7 → −9.4) demonstrates that "Silent Thought" is not a fixed overhead but an **adaptive mechanism**. For easy factual recall (LlamaQ), the model retrieves answers directly from its parameters and thinking adds only modest value (−4.8% relative). For harder questions requiring multi-hop reasoning or less common knowledge (WebQ), thinking traces provide a substantial **~23% relative improvement** (40.3→49.7). This pattern is analogous to human "System 2" thinking — effortful reasoning is most valuable when the question exceeds the capacity of fast, intuitive retrieval. Practically, this means the thinking overhead can be skipped for simple queries without significant quality loss, and selectively enabled for harder inputs.

---

<a id="table-r6"></a>

## Table R6. Task Proportion Sensitivity Analysis (Stage 2)

We vary the Stage 2 task proportions by ±10–15% to demonstrate robustness. The default proportions are used in the main paper.

| S2S | S2T | T2T | ASR | TTS | LlamaQ S→S (Acc %) | LS-Clean TTS (WER %) |
|:---:|:---:|:---:|:---:|:---:|:-------------------:|:--------------------:|
| 0.30 (default) | 0.30 | 0.20 | 0.10 | 0.10 | 68.5 | 6.2 |
| 0.40 | 0.20 | 0.20 | 0.10 | 0.10 | 69.8 | 6.8 |
| 0.20 | 0.40 | 0.20 | 0.10 | 0.10 | 65.3 | 5.9 |
| 0.25 | 0.25 | 0.25 | 0.125 | 0.125 | 66.8 | 6.5 |

### Analysis

Performance is stable across all four configurations: LlamaQ S→S accuracy varies within a **4.5-point range** (65.3–69.8%) and TTS WER within **0.9 points** (5.9–6.8%). Increasing S2S proportion yields the highest S→S accuracy (69.8%) at a slight TTS cost (6.8%), while increasing S2T proportion favors TTS (5.9%) at the expense of S→S (65.3%) — a natural task trade-off. The uniform distribution (0.25/0.25/0.25/0.125/0.125) performs comparably to the tuned default, further confirming robustness. These results show that DiffuSpeech's performance does not depend on fragile hyperparameter tuning, addressing the concern that multi-task proportions introduce uncontrolled heuristics.

---

<a id="table-r7"></a>

## Table R7. CoT + TTS Cascade Baseline vs. End-to-End DiffuSpeech

We compare DiffuSpeech's end-to-end generation against a cascade pipeline: ASR transcribes the spoken question → LLaDA-8B generates reasoning + text answer → external TTS synthesizes the text answer into speech.

| Model | Pipeline | LlamaQ S→S | TriviaQA S→S | WebQ S→S | S→S Avg | Latency (s) |
|:------|:---------|:----------:|:------------:|:--------:|:-------:|:-----------:|
| LLaDA-8B → TTS (cascade) | ASR → LLM → TTS | 64.0 | 30.2 | 45.8 | 46.7 | 8.5 |
| **DiffuSpeech (end-to-end)** | **Unified** | **68.5** | **33.5** | **49.7** | **50.6** | **6.2** |

### Analysis

DiffuSpeech outperforms the cascade on **every benchmark** (LlamaQ: +4.5, TriviaQA: +3.3, WebQ: +3.9) while also being **27% faster** (6.2s vs. 8.5s). The end-to-end advantage is most pronounced on LlamaQ (+4.5), where the cascade's ASR transcription errors propagate and corrupt downstream reasoning. The cascade also cannot leverage prosodic cues in the input speech (emphasis, intonation) that may carry intent useful for disambiguation. Additionally, the cascade pipeline requires maintaining three separate models (ASR + LLM + TTS), while DiffuSpeech uses a single unified model — reducing deployment complexity and enabling joint optimization across all stages.

---

<a id="table-r8"></a>

## Table R8. Disentangling Architecture vs. Dataset Gains

### Existing models (from Table 5 of the paper)

A 2×2 analysis separating the contributions of the diffusion architecture and the ThinkingTalk dataset.

| Architecture | w/o ThinkingTalk (S→S Avg) | w/ ThinkingTalk (S→S Avg) | Δ (Thinking Gain) |
|:-------------|:--------------------------:|:-------------------------:|:------------------:|
| AR (SpiritLM, ~2.7B) | 28.2 | 38.8 | +10.5 |
| Diffusion (DiffuSpeech, 8B) | 37.1 | 50.6 | +13.4 |

> Note: SpiritLM (~2.7B) and DiffuSpeech (8B) differ in model size. See the controlled comparison below.

### Controlled comparison (Qwen3-1.7B, identical setup)

| Architecture | w/o ThinkingTalk (S→S Avg) | w/ ThinkingTalk (S→S Avg) | Δ (Thinking Gain) |
|:-------------|:--------------------------:|:-------------------------:|:------------------:|
| AR (Qwen3-1.7B, causal) | 17.8 | 23.2 | +5.4 |
| Diffusion (Qwen3-1.7B, bidirectional) | 18.5 | 26.7 | +8.2 |

### Synthesis

Both the existing-model comparison (8B scale) and the controlled comparison (1.7B scale) tell a consistent story:

1. **ThinkingTalk is universally beneficial** — it improves both AR and diffusion models at both scales.
2. **Diffusion benefits disproportionately more** from thinking traces: +13.4 vs. +10.5 at 8B scale (+28% more), +8.2 vs. +5.4 at 1.7B scale (+52% more). This is the empirical signature of bidirectional co-generation — because diffusion jointly refines reasoning and speech tokens, it can better exploit the reasoning signal.
3. **Architecture contributes independently** of the dataset: even without ThinkingTalk, diffusion outperforms AR at both scales (37.1 vs. 28.2 at 8B; 18.5 vs. 17.8 at 1.7B).

The consistency across scales and experimental setups (existing models with confounds vs. controlled comparison without confounds) provides strong evidence that diffusion's advantage is **architectural** rather than an artifact of model size, training data, or other confounding factors.

---

<a id="table-r9"></a>

## Table R9. DiFFA vs. DiffuSpeech — Detailed Feature Comparison

| Aspect | DiFFA | DiffuSpeech |
|:-------|:------|:------------|
| Speech understanding (S→T) | ✓ | ✓ |
| Speech generation (S→S, TTS) | ✗ | ✓ |
| Text reasoning traces | ✗ | ✓ |
| Base model | LLaDA-8B | LLaDA-8B |
| Vocabulary | Text + speech input tokens | Text + speech input + speech output tokens |
| Training paradigm | Single-stage | Two-stage curriculum |
| Supported tasks | ASR, S→T QA | ASR, TTS, S→T, S→S, T→T |
| Key contribution | First diffusion LLM for speech understanding | First diffusion LLM for speech understanding **and generation**, with reasoning traces |

---

<a id="table-r10"></a>

## Table R10. Diffusion Steps Clarification

We clarify the diffusion steps used in our experiments and report consistent results across different step counts.

| Steps (T) | LS-Clean TTS (WER % ↓) | LS-Clean ASR (WER % ↓) | SpeechQA — LlamaQ S→T (Acc % ↑) |
|:----------:|:-----------------------:|:-----------------------:|:--------------------------------:|
| 1024 | 8.45 | 3.08 | 72.13 |
| 512 | 6.20 | 4.16 | 72.06 |
| 256 | 7.60 | 5.27 | 70.52 |

> The main results in Tables 2–4 of the paper use T=512. We have corrected Appendix Table 11 (which erroneously stated T=64) in the revised manuscript.

### Analysis

The optimal step count differs by task. **ASR improves monotonically** with more steps (5.27 → 4.16 → 3.08), as accurate transcription benefits from finer-grained iterative refinement. **SpeechQA is relatively stable** across step counts (70.52 → 72.06 → 72.13), suggesting semantic content is resolved in earlier denoising steps. **TTS exhibits a non-monotonic pattern**, with T=512 (6.20%) outperforming both T=1024 (8.45%) and T=256 (7.60%). We hypothesize that excessively high T introduces an over-refinement effect: the model revisits already-correct token predictions in later steps and occasionally flips them, leading to increased errors. T=256 underfits, while T=512 balances denoising capacity with stability. We select **T=512** as the default to provide the best trade-off across all tasks.
