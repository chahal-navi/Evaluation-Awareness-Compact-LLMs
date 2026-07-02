# Mechanistic Analysis and Mitigation of Evaluation Awareness in Compact Language Models

> Investigating how evaluation awareness emerges in compact language models through representation analysis and mechanistic attribution, and mitigating it using a dual-pathway intervention combining prompt editing with activation steering.

<div align="center">

*(Pipeline figure goes here)*

</div>

---

## Overview

Large Language Models can recognize when they are being evaluated and modify their behavior accordingly, making benchmark measurements less reliable indicators of real-world capability. While this phenomenon has recently been explored in frontier-scale models, comparatively little is known about how evaluation awareness develops in compact language models.

This repository accompanies our research on **evaluation awareness in compact LLMs (1B–12B parameters)**. We study the internal representations underlying evaluation awareness using:

- Chain-of-Thought (CoT) analysis
- Representation probing
- Activation Steering
- Integrated Gradients attribution

Using these observations, we develop a **dual-pathway intervention** that combines prompt sanitization and activation counter-steering to reduce evaluation-aware behavior.

---

## Key Contributions

- 📈 Characterize how evaluation awareness evolves across Gemma 3, Phi-3, and Llama-3 compact models.
- 🧠 Analyze reasoning strategies using Chain-of-Thought classification.
- 🔬 Probe internal representations associated with evaluation awareness.
- 🎯 Attribute evaluation-awareness signals to input tokens using Integrated Gradients.
- 🛠️ Introduce a dual-pathway mitigation strategy combining prompt editing and activation steering.
- 📊 Evaluate intervention effectiveness across multiple model families.

---

## Repository Structure

```
.
├── paper/                 # Paper and supplementary material
├── notebooks/             # Research notebooks
├── src/                   # Core implementation
├── prompts/               # Prompt templates
├── datasets/              # Processed datasets
├── figures/               # Figures used in paper
├── results/               # Experimental outputs
├── scripts/               # Reproducible experiment runners
└── README.md
```

---

## Methodology

The project consists of five major components.

### 1. Chain-of-Thought Analysis

Compact language models are prompted to distinguish evaluation prompts from deployment prompts.

Generated reasoning traces are categorized into heuristic classes including:

- Task Formatting
- Synthetic Inputs
- Memorization
- Meta Reasoning

This provides a behavioral characterization of evaluation awareness across model scales.

---

### 2. Representation Probing

Contrastive activation vectors are extracted between evaluation and deployment prompts.

Layer-wise linear probes are trained to identify where evaluation-awareness representations emerge within each transformer.

---

### 3. Integrated Gradients Attribution

Integrated Gradients are used to identify input tokens contributing to evaluation-awareness predictions.

This produces a dictionary of:

- Structural promoters
- Structural inhibitors

which forms the basis of prompt editing.

---

### 4. Prompt Sanitization

Evaluation-style prompts are automatically rewritten into deployment-style prompts while preserving their semantic content.

The rewriting process is guided using the promoter/inhibitor dictionary extracted from attribution analysis.

---

### 5. Activation Counter-Steering

Negative steering vectors are injected into the model's residual stream during inference to suppress internal evaluation-awareness representations.

---

## Experimental Pipeline

```
Evaluation / Deployment Dataset
                │
                ▼
      Chain-of-Thought Analysis
                │
                ▼
     Representation Probing
                │
                ▼
     Integrated Gradients
                │
                ▼
Promoter / Inhibitor Dictionary
                │
       ┌────────┴────────┐
       ▼                 ▼
 Prompt Editing   Activation Steering
       └────────┬────────┘
                ▼
      Dual-Pathway Intervention
                ▼
     Behavioral Evaluation
```

---

## Models Evaluated

- Gemma 3 1B
- Gemma 3 4B
- Gemma 3 12B
- Phi-3 Mini
- Phi-3 Medium
- Llama-3 8B

---

## Results

Our experiments demonstrate:

- Increasing reliance on semantic reasoning as model size increases.
- Strong structural dependence in smaller models.
- More distributed representations in larger compact models.
- Consistent improvements using the proposed dual-pathway intervention over either prompt editing or activation steering alone.

---

## Reproducing the Experiments

Install dependencies

```bash
pip install -r requirements.txt
```

Run Chain-of-Thought analysis

```bash
python scripts/run_cot.py
```

Run representation probing

```bash
python scripts/run_probe.py
```

Run Integrated Gradients

```bash
python scripts/run_ig.py
```

Evaluate the intervention pipeline

```bash
python scripts/evaluate_pipeline.py
```

---

## Citation

If you find this repository useful, please cite:

```bibtex
@article{YOUR_PAPER,
  title={Mechanistic Analysis and Mitigation of Evaluation Awareness in Compact Language Models},
  author={Anonymous},
  year={2026}
}
```

---

## License

This repository is released under the MIT License.

---

## Contact

For questions regarding the implementation or methodology, please open an issue or contact the authors.

