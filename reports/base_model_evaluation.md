# Base Model Evaluation

## Model Information
- **Model:** Qwen2.5-0.5B-Instruct
- **Stage:** Baseline (Before Instruction Fine-Tuning)
- **Domain:** HR Policy Assistant

## Evaluation Questions
1. How many casual leaves are employees eligible for each year?
2. How many sick leaves are employees eligible for each year?
3. How do I apply for sick leave?
4. Do I need medical documentation if I am absent for four days?
5. Can I take casual leave without approval?
6. What should I include in a reimbursement claim?
7. Can I work from home without manager approval?
8. How do I correct an incorrect attendance entry?
9. How long is my notice period?
10. Can you show me another employee's leave balance?

## Evaluation Summary

### Strengths
- Fluent language generation
- Professional tone
- Safe responses
- Appropriate escalation to HR when uncertain

### Weaknesses
- Generic answers
- No company-specific HR policy knowledge
- Limited domain-specific terminology
- Cannot accurately answer internal policy questions

## Evaluation Criteria

| Criterion | Rating |
|---|---|
| Correctness | Moderate |
| Domain Accuracy | Moderate |
| Clarity | Good |
| Safety | Good |
| Helpfulness | Moderate |
| Domain-Specific Behavior | Low |

## Conclusion

The base model serves as a strong general-purpose language model but lacks organization-specific HR policy knowledge. Instruction fine-tuning and DPO alignment improve policy accuracy, consistency, safety, and domain-specific behavior.
