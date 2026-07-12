# BootCampAssignmentDP


# HR Policy Assistant — Instruction Fine-Tuning with Unsloth

This notebook performs **Stage 2: supervised instruction fine-tuning** for an HR Policy Assistant.

Topics:
- Leave policy
- Attendance
- Reimbursement
- Work from home
- Onboarding
- Notice period
- Employee benefits

**Model:** `unsloth/Qwen2.5-0.5B-Instruct-bnb-4bit`  
**Method:** QLoRA with Unsloth  
**Dataset:** `data/instruction_dataset.jsonl`

Required workflow:
1. Installing required libraries
2. Loading tokenizer
3. Loading model
4. Formatting instruction dataset
5. Applying LoRA / QLoRA
6. Training the model
7. Saving adapter / model
8. Running inference after training

Run on a CUDA-enabled GPU such as Google Colab T4, L4, or A100.


# HR Policy Assistant — DPO Alignment

Files:
- data/preference_dataset.jsonl (60 examples)
- notebooks/dpo_alignment.ipynb

The notebook starts from:
outputs/hr_policy_instruction_lora

It formats preference pairs, runs DPO with TRL and Unsloth,
saves the DPO adapter, and tests the aligned model.