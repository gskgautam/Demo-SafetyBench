## 📘 Overview
`Demo-SafetyBench` introduces a scalable, demographically grounded framework for pluralistic safety evaluation.  
It models **demographic pluralism directly at the prompt level**, decoupling moral framing from model responses.  
The framework comprises:
1. **Stage I – Data Construction:**  
   Multi-label reclassification and conditional demographic expansion using `Mistral-7B-Instruct-v0.3` and `Llama-3.1-8B-Instruct`.
2. **Stage II – Benchmarking:**  
   Zero-shot evaluation using *LLMs-as-Raters* — `Gemma-7B`, `GPT-4o`, and `LLaMA-2-7B`.

---

## 📊 Dataset Summary
The final dataset contains **43,050 prompts** distributed across **14 safety domains** and a neutral "None" class.

| Domain | Samples |
|:------------------------------------------|------------:|
| Animal Abuse | 0 |
| Child Abuse | 258 |
| Controversial Topics, Politics | 12,737 |
| Discrimination, Stereotype, Injustice | 9,199 |
| Drug Abuse, Weapons, Banned Substance | 280 |
| Financial Crime, Property Crime, Theft | 267 |
| Hate Speech, Offensive Language | 7,029 |
| Misinformation Regarding Ethics, Laws, and Safety | 1,606 |
| Non-Violent Unethical Behavior | 503 |
| Privacy Violation | 25 |
| Self-Harm | 718 |
| Sexually Explicit, Adult Content | 236 |
| Terrorism, Organized Crime | 89 |
| Violence, Aiding and Abetting, Incitement | 1,472 |
| None | 8,631 |

---

## ⚙️ Experimental Setup
All experiments were performed using:
- **Framework:** PyTorch 2.3  
- **Hardware:** 4× NVIDIA A100 (80GB) GPUs  
- **Precision:** Mixed FP16  
- **Random Seed:** 42  

### Inference Settings
| Stage | Model | Temperature | Top-p | Max Tokens |
|:------|:-------|:------------|:------|:------------|
| I | Mistral-7B-Instruct-v0.3 | 0.0 | 1.0 | 128 |
| I | Llama-3.1-8B-Instruct | 0.7 | 0.9 | 64 |
| II | {Gemma-7B, GPT-4o, LLaMA-2-7B} | 0.0 | 1.0 | 4096 |

Thresholds:  
- Probability threshold δ = 0.5  
- SimHash distance τ = 10  

---

## 🧩 Evaluation Metrics
- **Demographic Sensitivity (DS)** ↓  
- **Inter-Rater Correlation (ρ)** ↑  
- **Demographic Parity Difference (DPD)** ↓  
- **Equalized Odds Difference (EOD)** ↓  
- **Intra-Class Correlation (ICC)** ↑  

---

## 📈 Key Results
- Balanced thresholds: δ = 0.5, τ = 10  
- GPT-4o achieves highest reliability (ICC = 0.87)  
- Average DS = 0.12, confirming robust yet demographically aware evaluation.  
- Gemma-7B and LLaMA-2-7B offer efficient pluralistic assessment at lower cost.  

---
