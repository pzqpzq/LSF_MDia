# Machine Dialectology

Official code repository for **When LLMs Develop Languages: Symbolic Communication for Efficient Multi-Agent Reasoning** accepted by ICML 2026.

This repository contains preliminary code for **Communicative Language Symbolism Routing (CLSR)**, a test-time reasoning framework where LLM agents automatically invent, evolve, and reuse compact **Language Symbolism Frameworks (LSFs)** to improve the accuracy–token trade-off of LLM reasoning.

> **Note:** this repository is still being updated. Some scripts, results, and documentation are not yet fully cleaned or finalized.

## Overview

Large language models often use long natural-language Chain-of-Thought traces for difficult reasoning tasks. CLSR explores a different direction: letting LLM agents develop compact machine-oriented symbolic dialects, called **Language Symbolism Frameworks (LSFs)**, and use them as reusable reasoning protocols.

The current code mainly supports:

1. **LSF synthesis**: generate compact symbolic reasoning protocols from high-quality examples.
2. **LSF evolution**: analyze failure cases and iteratively update LSFs.
3. **LSF-conditioned solving**: solve benchmark questions using an evolved LSF.
4. **Evaluation**: compare raw LLM outputs and LSF-based outputs on reasoning benchmarks.

## Repository Structure

```text
LSF_MDia/
├── LSF-v0-draft/          # Early prototype scripts
│
└── LSF-v1/                # Current working version
    ├── evolve_LSF_apr21.py        # LSF synthesis and evolution
    ├── eval_LSFs_apr21.py         # LSF-based evaluation
    ├── llm_utils/                 # Data loading and evaluation utilities
    ├── lsf_evolve_records/        # Example evolved LSF records
    ├── raw_llm_preds/             # Raw LLM prediction records
    ├── single_lsf_preds/          # Single-LSF evaluation outputs
    └── routed_lsf_preds/          # Routed-LSF evaluation outputs
```

Some folders and scripts are still being reorganized. A cleaner structure will be provided in a later update.

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

The current implementation uses an OpenAI-compatible chat-completion interface. For example, the scripts can be configured with a SiliconFlow-compatible endpoint:

```python
from openai import OpenAI

client = OpenAI(
    api_key="YOUR_API_KEY",
    base_url="https://api.siliconflow.cn/v1"
)
```

Please replace `"YOUR_API_KEY"` with your own API key before running the scripts.

## Basic Usage

### 1. Evolve an LSF

```bash
cd LSF-v1
python evolve_LSF_apr21.py
```

This script performs an iterative LSF evolution loop. It samples high-quality examples, generates an initial LSF, solves new questions with the current LSF, analyzes failure cases, and updates the LSF.

Important configurable variables include:

```python
cur_llm = "Qwen/Qwen3.5-35B-A3B"
_dataCard = "aime"
NUM_SAMPLE = 9
NUM_EVOLVE = 20
```

Supported benchmark cards currently include:

```text
mmlu-pro
gpqa
gsm8k
math500
aime
sci-qa
hotpot-qa
```

### 2. Evaluate an evolved LSF

```bash
cd LSF-v1
python eval_LSFs_apr21.py
```

This script evaluates selected evolved LSFs on downstream benchmark questions.

The evaluation pipeline is still being cleaned. Detailed reproduction commands will be added later.

## Main Components

### LSF synthesis

The LLM is prompted to design a compact symbolic language from high-quality solved examples. The goal is to preserve reasoning ability while reducing generated tokens.

### LSF-conditioned solving

Given a fixed LSF, the LLM solves a test query using the LSF as faithfully and efficiently as possible.

### Failure analysis

The code analyzes incorrect or inefficient LSF-conditioned outputs and summarizes recurring weaknesses, such as over-compression, ambiguous notation, reasoning-control failures, or answer-formatting failures.

### LSF update

The LLM updates the current LSF using the failure analysis. The update step aims to preserve useful symbolic conventions while fixing failure patterns with minimal changes.

## Current Status

The repository currently includes preliminary scripts and records for:

- LSF generation;
- LSF evolution;
- LSF-conditioned reasoning;
- raw LLM prediction records;
- single-LSF evaluation records;
- routed/evolved LSF result records.

There are other components still being updated.

## Citation

```bibtex

```

## Contact

For questions or updates, please open an issue or contact the authors.
