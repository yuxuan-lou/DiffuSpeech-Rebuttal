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
| ★ Qwen2.5-Omni | AR | | | | | | | | | | |
| ★ Qwen3-Omni | AR | | | | | | | | | | |
| ★ GLM-4-Voice | AR | | | | | | | | | | |
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
| ★ Qwen2.5-Omni | AR | | | | | | |
| ★ Qwen3-Omni | AR | | | | | | |
| ★ GLM-4-Voice | AR | | | | | | |
| DiFFA | Diff. | — | / | — | / | — | 29.6 |
| **DiffuSpeech** | **Diff.** | **3.0** | **6.2** | **7.1** | **10.3** | **66.2** | **39.0** |

---

<a id="table-r2"></a>

## Table R2. Controlled AR vs. Diffusion Comparison (Qwen3-1.7B)

To rigorously isolate the effect of the generation paradigm (AR vs. Diffusion), we conduct a strictly controlled experiment. Both variants use the **Qwen3-1.7B dense architecture** with **random initialization**. The **only** difference is the attention mechanism: causal (unidirectional) for AR vs. bidirectional for Diffusion. All other factors — tokenizer, vocabulary, speech tokens, training data, hyperparameters, and training steps — are identical. Both models are trained through Stage 1 (speech-text alignment) and Stage 2 (ThinkingTalk instruction following).

| Model | Attention | LlamaQ S→S | TriviaQA S→S | WebQ S→S | S→S Avg | LS-Clean ASR | LS-Clean TTS |
|:------|:----------|:----------:|:------------:|:--------:|:-------:|:------------:|:------------:|
| Qwen3-1.7B (AR) | Causal | | | | | | |
| Qwen3-1.7B (Diff.) | Bidirectional | | | | | | |

### With vs. Without ThinkingTalk (Controlled 2×2)

| Model | Attention | w/o ThinkingTalk S→S Avg | w/ ThinkingTalk S→S Avg | Δ (Thinking Gain) |
|:------|:----------|:------------------------:|:-----------------------:|:------------------:|
| Qwen3-1.7B (AR) | Causal | | | |
| Qwen3-1.7B (Diff.) | Bidirectional | | | |

---

<a id="table-r3"></a>

## Table R3. Inference Latency Comparison

Wall-clock latency measured on a single GPU for generating a response to a typical spoken question (~5 seconds input, ~10 seconds output). DiffuSpeech is evaluated both with vanilla inference and with [Fast-dLLM v2](https://github.com/NVlabs/Fast-dLLM) acceleration (KV cache + confidence-aware parallel decoding), a training-free inference acceleration framework for diffusion LLMs.

| Model | Method | Time-to-First-Audio (s) | Total Generation Time (s) | RTF |
|:------|:-------|:-----------------------:|:-------------------------:|:---:|
| DiffuSpeech | Vanilla | | | |
| DiffuSpeech | + Fast-dLLM v2 | | | |
| Moshi | — | | | |
| MinMo | — | | | |
| Qwen3-Omni | — | | | |

> RTF = Real-Time Factor (generation time / audio duration). Lower is better.

---

<a id="table-r4"></a>

## Table R4. Reasoning Evaluation in Text-in, Text-out (T→T) Mode

We evaluate DiffuSpeech in T→T mode on challenging reasoning benchmarks to assess whether multi-task speech-text training preserves hard reasoning capabilities.

| Model | Type | GSM8K | MATH | HumanEval |
|:------|:-----|:-----:|:----:|:---------:|
| LLaDA (base model) | Diff. | 70.3 | | |
| **DiffuSpeech** | **Diff.** | **72.8** | | |
| Phi-4-Multimodal | AR | 88.6 | | |
| MinMo | AR | 58.1 | | |

---

<a id="table-r5"></a>

## Table R5. Inference Reasoning Ablation: With vs. Without Thinking Traces

At inference time, we disable thinking traces (skip the thinking segment) to measure the benefit of "Silent Thought" across benchmarks of varying difficulty.

| Benchmark | Difficulty | With Thinking | Without Thinking | Δ |
|:----------|:----------|:-------------:|:----------------:|:---:|
| LlamaQ | Easy | 68.5 | | |
| TriviaQA | Medium | 33.5 | | |
| WebQ | Hard | 49.7 | | |

---

<a id="table-r6"></a>

## Table R6. Task Proportion Sensitivity Analysis (Stage 2)

We vary the Stage 2 task proportions by ±10–15% to demonstrate robustness. The default proportions are used in the main paper.

| S2S | S2T | T2T | ASR | TTS | LlamaQ S→S (Acc %) | LS-Clean TTS (WER %) |
|:---:|:---:|:---:|:---:|:---:|:-------------------:|:--------------------:|
| 0.30 (default) | 0.30 | 0.20 | 0.10 | 0.10 | 68.5 | 6.2 |
| 0.40 | 0.20 | 0.20 | 0.10 | 0.10 | | |
| 0.20 | 0.40 | 0.20 | 0.10 | 0.10 | | |
| 0.25 | 0.25 | 0.25 | 0.125 | 0.125 | | |

---

<a id="table-r7"></a>

## Table R7. CoT + TTS Cascade Baseline vs. End-to-End DiffuSpeech

We compare DiffuSpeech's end-to-end generation against a cascade pipeline: ASR transcribes the spoken question → LLaDA-8B generates reasoning + text answer → external TTS synthesizes the text answer into speech.

| Model | Pipeline | LlamaQ S→S | TriviaQA S→S | WebQ S→S | S→S Avg | Latency (s) |
|:------|:---------|:----------:|:------------:|:--------:|:-------:|:-----------:|
| LLaDA-8B → TTS (cascade) | ASR → LLM → TTS | | | | | |
| **DiffuSpeech (end-to-end)** | **Unified** | **68.5** | **33.5** | **49.7** | **50.6** | |

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
| AR (Qwen3-1.7B, causal) | | | |
| Diffusion (Qwen3-1.7B, bidirectional) | | | |

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
| 64 | | | |

> The main results in Tables 2–4 of the paper use T=512. We have corrected Appendix Table 11 (which erroneously stated T=64) in the revised manuscript. The counter-intuitive improvement from T=1024 to T=512 on TTS is discussed in Section 5.3 of the revised paper.
