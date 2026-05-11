# Machine Dialectology

Code repository for **LLM-generated symbolic languages for efficient reasoning**.

This repository currently contains two closely related lines of work:

1. **CLSR**: a framework called Communicative Language Symbolism Routing, associated with our ICML 2026 paper  
   **When LLMs Develop Languages: Symbolic Communication for Efficient Multi-Agent Reasoning**.

2. **MDia**: an upgraded and more general framework, tentatively titled  
   **Machine Dialectology**, which extends CLSR to multi-model, multi-agent, and cross-category symbolic language evolution.

> **Note:** this repository is still being updated. Some scripts, results, and reproduction instructions are not yet fully cleaned or finalized.

## Overview

Large language models often rely on long natural-language Chain-of-Thought traces for difficult reasoning tasks. This repository explores an alternative direction: letting LLM agents develop compact machine-oriented symbolic dialects, called **Language Symbolism Frameworks (LSFs)**, and use them as reusable reasoning protocols.

The core idea is that LLMs may not need to express all reasoning steps in verbose natural language. Instead, they can develop compact symbolic conventions that preserve reasoning ability while reducing generated tokens.

## Repository Structure

```text
LSF_MDia/
├── LSF-v0-draft/          # Early prototype scripts for CLSR
│  
└── LSF-v1/                # MDia prototype: generalized Machine Dialectology framework
    ├── evolve_LSF_apr21.py
    ├── eval_LSFs_apr21.py
    ├── llm_utils/
    ├── lsf_evolve_records/
    ├── raw_llm_preds/
    ├── single_lsf_preds/
    └── routed_lsf_preds/
```

## CLSR: ICML 2026 Version

CLSR, short for **Communicative Language Symbolism Routing**, studies how LLM agents can generate and evolve compact symbolic reasoning protocols.

In CLSR, a specific type of LLM agent first generates initial LSFs from exemplars. These LSFs are then used to produce responses, and the system iteratively refines the symbolic protocols based on correctness and token efficiency.

The basic CLSR workflow is:

1. sample exemplar questions and answers;
2. generate initial LSFs;
3. use the LSFs to answer benchmark questions;
4. select concise and correct responses;
5. iteratively evolve the LSFs;
6. evaluate the final LSFs on reasoning benchmarks.

## MDia: Machine Dialectology

`LSF-v1/` is an upgraded version of CLSR, tentatively named **MDia** or **Machine Dialectology**.

MDia generalizes CLSR from a single-type LLM-agent setting to a broader multi-agent and cross-category setting. Instead of first generating initial LSFs from exemplars, MDia lets multiple types of LLM agents directly attempt the query, collects the most concise and correct responses across different models, and then lets agents discuss and synthesize suitable LSFs for their own reasoning styles.

The high-level MDia workflow is:

1. multiple heterogeneous LLM agents answer the query directly;
2. concise and correct responses are selected across agents;
3. agents discuss these high-leverage responses;
4. each agent generates or updates its own LSF;
5. agents solve new queries using their corresponding LSFs;
6. collective discussion and routing further refine the dialect pool.

MDia also introduces **cross-category routing**, where symbolic dialects can be selected or transferred across different task categories.


## CLSR vs. MDia

| Aspect | CLSR | MDia / Machine Dialectology |
|---|---|---|
| Main status | ICML 2026 accepted paper | Ongoing journal-level extension |
| Core idea | LLM-generated LSFs for efficient reasoning | Machine dialectology across heterogeneous LLM agents |
| Agent setting | A specific type of LLM agent | Multiple different types of LLM agents |
| Initial step | Generate initial LSFs from exemplars | Agents first answer queries directly |
| Evolution signal | Correct and concise LSF-conditioned responses | Correct and concise responses collected across heterogeneous agents |
| Discussion pattern | Same-type LLM-to-LLM refinement | Cross-model and cross-category discussion |
| Routing | LSF routing for reasoning efficiency | Cross-category and cross-agent dialect routing |
| Experimental scope | ICML version experiments | Broader and larger-scale LLM experiments |

In short, **MDia can be viewed as a generalization of CLSR**. CLSR focuses on symbolic communication routing for efficient reasoning, while MDia studies a broader setting in which different LLM communities develop, exchange, and route machine dialects.

## Installation

Clone the repository:

```bash
git clone https://github.com/pzqpzq/LSF_MDia.git
cd LSF_MDia
```

Install basic dependencies:

```bash
pip install openai
```

A finalized `requirements.txt` will be added later.

## API Setup

The current scripts use an OpenAI-compatible chat-completion interface. For example, some scripts are configured with a SiliconFlow-compatible endpoint:

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_API_KEY",
    base_url="https://api.siliconflow.cn/v1"
)
```

Please replace `"YOUR_API_KEY"` with your own API key before running the scripts.

## Basic Usage

```bash
cd LSF-v1
python evolve_LSF_apr21.py
```

To evaluate evolved LSFs:

```bash
python eval_LSFs_apr21.py
```

The MDia implementation is still under active development. Some scripts and outputs are preliminary.

## Benchmarks

The current codebase is organized around several reasoning benchmarks, including:

```text
mmlu-pro
gpqa
gsm8k
math500
aime
sci-qa
hotpot-qa
```

More complete dataset preparation and preprocessing instructions will be added later.

## Current Status

This repository currently includes:

- preliminary CLSR code for the accepted ICML 2026 paper;
- early MDia code for Machine Dialectology;
- LSF generation and evolution scripts;
- LSF-conditioned evaluation scripts;
- raw LLM prediction records;
- single-LSF and routed-LSF result folders.

There are other components still being updated...


## Citation

If you use the CLSR code, please cite:

```bibtex
```

## Contact

For questions, please open an issue or contact the authors.
