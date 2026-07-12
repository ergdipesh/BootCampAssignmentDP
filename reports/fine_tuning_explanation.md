# Fine-Tuning Explanation

## Overview

This project builds an **HR Policy Assistant** by adapting an open-source Large Language Model (LLM) using **Unsloth** in three stages:

1. Non-Instruction Fine-Tuning
2. Instruction Fine-Tuning (Supervised Fine-Tuning, SFT)
3. Direct Preference Optimization (DPO)

The objective is to transform a general-purpose language model into a domain-specific assistant that provides accurate, professional, and safe HR policy answers.

---

## Base Model

The starting model is:

- **Qwen2.5-0.5B-Instruct**
- Loaded in **4-bit** precision using **Unsloth**
- Adapted using **QLoRA (Quantized Low-Rank Adaptation)**

The base model already understands natural language but does not know an organization's internal HR policies.

---

## Stage 1 – Non-Instruction Fine-Tuning

### Goal

Teach the model HR terminology, writing style, and policy language before teaching question answering.

### Dataset

A raw HR policy corpus containing narrative policy text, such as:

- Leave policy
- Attendance
- Reimbursement
- Work from home
- Onboarding
- Notice period
- Employee benefits

### Process

1. Clean the policy text.
2. Split it into training chunks.
3. Tokenize the text.
4. Train using QLoRA.
5. Save the LoRA adapter.

### Outcome

The model becomes familiar with HR vocabulary and policy wording but is not yet optimized for answering employee questions.

---

## Stage 2 – Instruction Fine-Tuning (SFT)

### Goal

Teach the model how to answer employee questions.

### Dataset

Instruction–response pairs in JSONL format:

```json
{
  "instruction": "How do I apply for sick leave?",
  "response": "Apply through the HR portal by selecting Sick Leave and submitting the required information."
}
```

### Process

1. Load the Stage 1 model (or base model for an independent run).
2. Format examples using the model's chat template.
3. Apply LoRA/QLoRA.
4. Train with TRL's `SFTTrainer`.
5. Save the adapter.

### Outcome

The model learns to provide direct, structured, and policy-specific answers instead of generic guidance.

---

## Stage 3 – Direct Preference Optimization (DPO)

### Goal

Improve response quality by teaching the model which answer is preferred.

### Dataset

Each example contains:

- Prompt
- Chosen response
- Rejected response

Example:

```json
{
  "prompt": "Can I work from home without approval?",
  "chosen": "No. Work-from-home requests require manager approval.",
  "rejected": "Yes. Work from home whenever you want."
}
```

### Process

1. Load the SFT model.
2. Format prompt, chosen, and rejected responses.
3. Configure `DPOTrainer`.
4. Train using preference pairs.
5. Save the aligned adapter.

### Outcome

The model learns to prefer answers that are:

- Correct
- Helpful
- Safe
- Professional
- Domain-specific

while avoiding inaccurate, unsafe, or overly generic responses.

---

## Why Use LoRA / QLoRA?

LoRA trains only a small number of additional parameters instead of updating the entire model.

Benefits:

- Lower GPU memory usage
- Faster training
- Smaller adapters
- Easy deployment

QLoRA extends LoRA by loading the base model in 4-bit precision, enabling fine-tuning on consumer GPUs.

---

## Why Use Unsloth?

Unsloth provides:

- Faster fine-tuning
- Lower memory consumption
- Optimized QLoRA implementation
- Compatibility with Hugging Face Transformers and TRL

This makes it well suited for educational and production experiments on smaller GPUs.

---

## Training Pipeline

```
Base Model
      │
      ▼
Non-Instruction Fine-Tuning
      │
      ▼
Instruction Fine-Tuning (SFT)
      │
      ▼
Direct Preference Optimization (DPO)
      │
      ▼
Final HR Policy Assistant
```

---

## Improvements Across Stages

| Stage | Main Improvement |
|-------|------------------|
| Base Model | General language understanding |
| Non-Instruction FT | Learns HR terminology and writing style |
| SFT | Learns to answer HR policy questions |
| DPO | Produces safer, more accurate, and more helpful responses |

---

## Best Practices

- Use high-quality domain data.
- Validate all policy content with HR experts.
- Keep policies updated.
- Evaluate on unseen questions.
- Combine the final model with Retrieval-Augmented Generation (RAG) so current HR documents remain the source of truth.

---

## Conclusion

The three-stage fine-tuning approach progressively improves the model:

- Stage 1 builds domain familiarity.
- Stage 2 teaches task-specific question answering.
- Stage 3 aligns responses with preferred behavior.

The resulting HR Policy Assistant is more accurate, consistent, and reliable than the original base model while remaining computationally efficient through Unsloth and QLoRA.
