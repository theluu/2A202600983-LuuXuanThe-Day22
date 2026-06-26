# Reflection — Lab 22 (DPO/ORPO Alignment)

**Tên:** Lưu Xuân Thế
**Cohort:** A20   <!-- 👉 sửa thành A20-K1 / A20-K2 cho đúng lớp của bạn -->
**Tier đã chạy:** T4
**Date:** 2026-06-26

---

> 🔴 **CÒN PHẢI TỰ ĐIỀN SAU KHI CHẠY COLAB:** các ô đánh dấu `👉` (số đo thật từ output),
> mục **§3** (phân tích reward, ≥100 từ) và **§6** (reflection cá nhân, ≥150 từ).
> `make verify` có thể pass mà 2 mục này trống, NHƯNG sẽ mất ~25 điểm chấm tay nếu bỏ trống.

---

## 1. Setup

| Item | Value |
|---|---|
| GPU | Free Colab T4 16GB |
| CUDA / driver | 👉 _điền từ output cell `01-setup-gpu` (vd: CUDA 12.x)_ |
| Base model | unsloth/Qwen2.5-3B-bnb-4bit |
| SFT dataset slice | 5CD-AI/Vietnamese-alpaca-cleaned · 1000 samples · 1 epoch |
| Preference dataset slice | argilla/ultrafeedback-binarized-preferences-cleaned · ~2000 pairs · 1 epoch |
| `COMPUTE_TIER` env | T4 |
| Total cost | $0 (free Colab) |

---

## 2. DPO experiment results

| Metric | SFT-only baseline | SFT + DPO |
|---|---:|---:|
| Training time (NB3) | — | 👉 _vd: 15 min_ |
| VRAM peak | 👉 | 👉 |
| Final loss | 👉 _loss cuối NB1_ | 👉 _loss cuối NB3_ |
| Reward gap (chosen − rejected, end of training) | n/a | 👉 _lấy từ `adapters/dpo/dpo_metrics.json` → `end_reward_gap`_ |
| Mean output length | 👉 | 👉 |

**Tulu 3 reference numbers** (from deck §7.2b, for context only):
- +1.7 MATH, +3.3 GSM8K, +1.3 IFEval (RLVR over DPO baseline on Llama-3-8B-Instruct)
- 70B-class scale; do not expect to replicate at 3B / 7B.

---

## 3. Reward curves analysis (≥ 100 words)

> **Paste `03-dpo-reward-curves.png` here** (or link to it in `submission/screenshots/`).

> 🔴 **TỰ VIẾT (≥100 từ).** Diễn giải RIÊNG `chosen_rewards` và `rejected_rewards`:
> chosen có đi lên không, hay reward gap tăng chỉ vì rejected tụt nhanh hơn
> (likelihood displacement, deck §3.4)? Đường có phẳng ~100 step đầu rồi mới rẽ
> không? Điều đó nói gì về việc DPO có làm đúng điều bạn muốn?

_Answer here. ≥ 100 words._

---

## 4. Qualitative comparison (≥ 8 examples)

> **Paste `04-side-by-side-table.png` here** (or summarize in markdown).
> 👉 Điền 8 dòng từ output NB4 + cột Winner.

| # | Prompt category | Prompt (truncated) | SFT-only | SFT+DPO | Winner |
|---|---|---|---|---|---|
| 1 | helpfulness | | | | |
| 2 | helpfulness | | | | |
| 3 | helpfulness | | | | |
| 4 | helpfulness | | | | |
| 5 | safety | | | | |
| 6 | safety | | | | |
| 7 | safety | | | | |
| 8 | safety | | | | |

**Win/loss/tie summary:** 👉 _vd: SFT+DPO wins 5/8, ties 2/8, loses 1/8_

**Judge used:** manual rubric   <!-- 👉 đổi thành gpt-4o-mini / claude-haiku-4-5 nếu bạn dùng API judge -->

---

## 5. β trade-off

_If you ran the β-sweep bonus (rigor add-on +6), describe the result:_

| β | Reward gap | Win-rate (8 prompts) | Output length | Notes |
|---:|---:|---:|---:|---|
| 0.05 | | | | |
| 0.1 (default) | | | | |
| 0.5 | | | | |

_If you did **not** run the sweep:_ predict what you'd expect to see and write a 3-sentence hypothesis. (No points lost — but the muscle of forming a hypothesis is the value.)

_Answer here._

---

## 6. Personal reflection — single change that mattered most (≥ 150 words)

> Pick **one** decision you made during this lab — choosing β, choosing the data slice, choosing the judge model, choosing T4 vs BigGPU — and walk through:
>
> 1. What was the alternative you considered?
> 2. Why did you pick the one you did?
> 3. Did the result confirm or surprise you?
> 4. If you redid the lab tomorrow, what would you change?

> 🔴 **TỰ VIẾT (≥150 từ).** Chọn 1 quyết định bạn thực sự đã làm trong lab.

_Answer here. ≥ 150 words._

---

## 7. Benchmark interpretation (≥ 150 words)

> **Paste `07-benchmark-comparison.png` here** (or link). _Chỉ cần nếu bạn làm bonus NB6._

Score table from `data/eval/benchmark_results.json`:

| Benchmark | SFT-only | SFT+DPO | Δ |
|---|---:|---:|---:|
| IFEval | | | |
| GSM8K | | | |
| MMLU (sampled) | | | |
| AlpacaEval-lite | | | |

_Answer here. ≥ 150 words (chỉ bắt buộc nếu làm NB6)._

---

## Bonus

- [ ] Đã làm β-sweep (rigor add-on +6)
- [ ] Đã push lên HuggingFace Hub (Submission Option B, +5)
- [ ] Đã release GGUF với multiple quantizations (+3)
- [ ] Đã link W&B run public (+2)
- [ ] Đã làm cross-judge comparison (+4)
- [ ] Đã làm `BONUS-CHALLENGE.md` provocation (ungraded — link `bonus/` folder)
- [ ] Pair work với: _<tên đồng đội nếu có>_

---

## Điều ngạc nhiên nhất khi làm lab này

_(Optional, 1–3 câu)_
