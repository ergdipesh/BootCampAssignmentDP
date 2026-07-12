# Final Evaluation Report

## Project
**Domain:** HR Policy Assistant  
**Base Model:** Qwen2.5-0.5B-Instruct  
**Framework:** Unsloth  
**Training Pipeline:**
1. Non-Instruction Fine-Tuning
2. Instruction Fine-Tuning (SFT)
3. Direct Preference Optimization (DPO)

---

## Evaluation Overview

Three versions of the model were evaluated:

| Model | Purpose |
|---|---|
| Base Model | General-purpose language model before domain adaptation |
| SFT Model | Learns HR policies and answers employee questions |
| DPO Model | Learns preferred responses to improve quality, safety, and helpfulness |

---

## Evaluation Criteria

- Correctness
- Domain Accuracy
- Clarity
- Safety
- Helpfulness
- Less Generic Responses
- Better Domain-Specific Behavior

---

## Overall Comparison

| Criterion | Base Model | SFT Model | DPO Model |
|---|---|---|---|
| Correctness | Moderate | Good | Excellent |
| Domain Accuracy | Moderate | Excellent | Excellent |
| Clarity | Good | Excellent | Excellent |
| Safety | Good | Very Good | Excellent |
| Helpfulness | Moderate | Excellent | Excellent |
| Less Generic | Low | High | Very High |
| Domain-Specific Behavior | Low | High | Very High |

---

## Observations

### Base Model
**Strengths**
- Fluent and professional.
- Handles general HR questions safely.
- Escalates uncertain topics to HR.

**Limitations**
- Generic responses.
- Does not know organization-specific policies.
- Limited procedural guidance.

### Instruction Fine-Tuned Model
**Improvements**
- Correct HR terminology.
- Policy-specific answers.
- Better procedural guidance.
- More actionable responses.

### DPO-Aligned Model
**Additional Improvements**
- Chooses safer responses.
- Avoids unsupported or fabricated policy statements.
- Better privacy protection.
- More professional and consistent tone.
- Better distinguishes when to escalate to HR.

---

## Example Progression

**Question:** How do I apply for sick leave?

**Base Model**
> Inform your manager and follow your company's leave process.

**SFT Model**
> Apply through the HR portal by selecting Sick Leave and submitting the required information.

**DPO Model**
> Apply through the HR portal by selecting Sick Leave, enter the required dates and details, attach medical documentation if requested, and notify your manager according to company policy.

---

## Final Assessment

| Model | Overall Rating |
|---|---|
| Base Model | ⭐⭐⭐☆☆ |
| Instruction Fine-Tuned | ⭐⭐⭐⭐☆ |
| DPO-Aligned | ⭐⭐⭐⭐⭐ |

---

## Conclusion

The three-stage training pipeline significantly improved the HR Policy Assistant.

Compared with the base model, the final DPO-aligned model provides:

- More accurate HR policy answers
- Better domain-specific reasoning
- Clearer and more actionable guidance
- Improved safety and privacy handling
- More consistent professional responses
- Reduced generic or ambiguous answers

For production deployment, the DPO-aligned model should be combined with retrieval-augmented generation (RAG) so that changing HR policies are retrieved from the latest approved documents rather than relying solely on model parameters.

---

## Final Recommendation

Deploy the **DPO-aligned HR Policy Assistant** as the preferred model for employee HR-policy questions, while integrating it with an authoritative HR knowledge base for up-to-date policy retrieval and governance.
