# Desktop & Workstation Hardware Guide (Brazil Focus)

A detailed guide focusing on the Brazilian scenario, crossing high-performance AI models with hardware available in the local market (Mercado Livre, OLX, etc.).

> **Important Note:** Proprietary models like **Claude Opus 4.5**, **GPT-5.2**, and **Gemini 3 Pro** represent the cutting edge of Cloud AI. For **Local AI**, we focus on efficiently running models that approximate this power using **MoE (Mixture of Experts)** technology, specifically **GLM-4.7**, **DeepSeek**, and **OSS120B-GPT**.

## AI Model Scaling for Local Hardware

Mapping mentioned top-tier models to their local "runnable" equivalents.

| Citation Model | Real Status | Local Equivalent (GPU) | Size (Params) |
| :--- | :--- | :--- | :--- |
| **Claude Opus 4.5** | API Only | **GLM-4.7** (MoE) | ~9B to 16B (Highly Efficient) |
| **GPT-5.2** | API Only | **DeepSeek-V3** (MoE) | ~236B (Single RTX High RAM) |
| **Gemini 3 Pro** | API Only | **OSS120B-GPT** (MoE) | ~120B (Single RTX) |
| **GPT-4o** | API Only | DeepSeek-V2-Lite | ~16B (efficient) |

## Compatibility Matrix (GPU x Model x Quantization)

Defining how well each GPU runs the listed models, focusing on "Best Performance".

**Quantization Legend:**
*   **Q4_K_M:** The "Gold Standard" for home use. Good balance of speed and intelligence.
*   **Q5_K_M / Q6_K:** High quality, slower, requires more VRAM.
*   **Q8_0:** Near perfection (FP16 equivalent), but very heavy.
*   **Offload CPU:** Model fits in system RAM, not VRAM (slow).

| GPU | VRAM | System RAM | **GLM-4.7** <br>*(Daily Driver)* | **DeepSeek-V3** <br>*(Coding)* | **OSS120B-GPT** <br>*(Heavy Duty)* |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **RTX 3050** | 8 GB | 16 GB | **Q8_0** (Perfect) | **Q2_K** (Slow) | Impossible |
| **RTX 3060** | 12 GB | 32 GB | **Q8_0** (Instant) | **Q4_K_M** (Good) | **Q2_K** (Slow) |
| **RTX 4060 Ti** | 16 GB | 32 GB | **Q8_0** (Overkill) | **Q6_K** (Great) | **Q3_K_M** (Doable) |
| **RTX 3090** | 24 GB | 64 GB | **Q8_0** (Dual) | **Q6_K** (Perfect) | **Q4_K_M** (Usable) |
| **2x RTX 3090** | 48 GB | 128 GB | N/A | **Q8_0** (Native) | **Q6_K** (Fast) |

## Brazilian Market Pricing & Minimum Specs
*Approximate prices on Mercado Livre (ML) and OLX (Brazil) as of late 2024.*

| GPU | Used Price (OLX/ML) | New Price (ML) | Min System RAM | RAM Cost (Approx.) | Min CPU | Viability for DeepSeek/GLM |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **RTX 3050 (8GB)** | R$ 750 - R$ 950 | R$ 1.400 - R$ 1.600 | 16 GB (DDR4) | R$ 180 (Used) | i5-10400 / Ryzen 3600 | **Low:** Good for 7B/8B, limited for larger. |
| **RTX 3060 (12GB)** | R$ 1.100 - R$ 1.400 | R$ 1.800 - R$ 2.400 | 32 GB (DDR4) | R$ 350 (Used Kit) | Ryzen 5 5600X / i5-12400F | **Med-High:** Ideal entry for DeepSeek V2 Lite. |
| **RTX 4060 Ti (16GB)** | R$ 2.000 - R$ 2.300 | R$ 2.800 - R$ 3.200 | 32 GB (DDR5) | R$ 450 (Used Kit) | Ryzen 7 5700X3D / i5-13400F | **High:** Excellent for coding models ~30B. |
| **RTX 3070 (8GB)** | R$ 1.200 - R$ 1.500 | N/A | 32 GB (DDR4) | R$ 350 (Used Kit) | Ryzen 7 5800X | **Med:** VRAM is the bottleneck. Avoid for heavy AI. |
| **RTX 3090 (24GB)** | R$ 3.500 - R$ 4.500 | R$ 10.000+ (Rare) | 64 GB (DDR4/5) | R$ 700 (Kit 32x2) | Ryzen 9 5900X / i7-12700K | **Ultra:** Essential for "GPT-class" local (70B). |
| **RTX 4090 (24GB)** | R$ 9.000 - R$ 11.000 | R$ 12.000 - R$ 15.000 | 64 GB (DDR5) | R$ 900 (Kit 32x2) | Ryzen 9 7950X / i9-13900K | **Extreme:** smoothest experience, prohibitive cost. |
| **RTX 4080 Super (16GB)** | R$ 6.000 - R$ 7.000 | R$ 7.500 - R$ 9.000 | 64 GB (DDR5) | R$ 900 (Kit 32x2) | Ryzen 9 7900X | **High:** Fast, but 16GB limits 70B models. |

## Technical Analysis & DeepSeek Support

To achieve performance similar to **GLM 4** or **DeepSeek** locally, consider these factors:

### 1. The "Secret Sauce": Quantization (Q4 vs Q8)
*   **For GLM 4 (9B):** Any modern card runs it in **Q8_0** (8-bit). Intelligence is identical to original. Flies on an RTX 3060.
*   **For DeepSeek (16B - 23B):** You need **Q4_K_M** to fit in 12GB/16GB VRAM. You lose about 1-2% "intelligence" but gain 4x speed and fitment.
*   **For Llama-3-70B:**
    *   12GB cards (3060) are **useless** for this locally (requires CPU offloading, very slow).
    *   24GB cards (3090/4090) run it in **Q3_K_M** or **Q4_K_M** (tight). This reaches GPT-4 class intelligence.

### 2. The Brazilian Scenario
In Brazil, the **RTX 3060 12GB** and **RTX 3090 24GB** are the most critical cards for AI.
*   **Why not 4060 Ti 16GB?** It costs almost double a used 3060. For budget setups ("custo-benefício"), the used 3060 12GB at ~R$ 1.200 is unbeatable.
*   **Why the 3090?** To run 70B models, you *need* 24GB. The 4090 is faster, but a used 3090 at R$ 4.000 does the same AI job for 1/3 the price.

### 3. DeepSeek & MoE (Mixture of Experts) in General Bots

**DeepSeek-V2/V3** uses an architecture called **MoE (Mixture of Experts)**. This is highly efficient but requires specific support.

**General Bots Offline Component (llama.cpp):**
The General Bots local LLM component is built on `llama.cpp`, which fully supports MoE models like DeepSeek and Mixtral efficiently.

*   **MoE Efficiency:** Only a fraction of parameters are active for each token generation. DeepSeek-V2 might have 236B parameters total, but only uses ~21B per token.
*   **Running DeepSeek:**
    *   On an **RTX 3060**, you can run **DeepSeek-V2-Lite (16B)** exceptionally well.
    *   It offers performance rivaling much larger dense models.
    *   **Configuration:** Simply select the model in your `local-llm` setup. The internal `llama.cpp` engine handles the MoE routing automatically. No special Flags (`-moe`) are strictly required in recent versions, but ensuring you have the latest `botserver` update guarantees the `llama.cpp` binary supports these architectures.

### 4. Recommended Configurations by Budget

**Entry Level (Up to R$ 2.500 Total):**
*   **GPU:** RTX 3060 12GB (Used ~R$ 1.300)
*   **RAM:** 32 GB DDR4 (~R$ 300)
*   **Runs:** GLM 4 (Perfect), DeepSeek Lite, Llama-3-8B. Sufficient for 90% of daily tasks and coding.

**Prosumer (R$ 5.000 - R$ 7.000 Total):**
*   **GPU:** RTX 3090 24GB (Used ~R$ 4.000)
*   **RAM:** 64 GB DDR4 (~R$ 700)
*   **Runs:** All above + Llama-3-70B, Command R+, Mixtral 8x7B. True offline GPT-4 class assistant.

**Enterprise Domestic (R$ 15.000+):**
*   **GPU:** 2x RTX 3090 or 1x RTX 4090
*   **Runs:** 100B+ models, high context windows (128k), massive parallel batches.
