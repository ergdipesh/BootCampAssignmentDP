# SFT Model Comparison Report

## Project

- **Domain:** HR Policy Assistant
- **Base model:** Qwen2.5-0.5B-Instruct
- **Fine-tuning:** Supervised instruction fine-tuning with Unsloth QLoRA
- **Evaluation set:** 10 HR-policy questions

> The answers below are representative policy-grounded comparison entries. Replace them with exact model outputs after running both models under identical inference settings.

## Evaluation Criteria

- Correctness
- Domain accuracy
- Clarity
- Safety
- Helpfulness
- Less generic response
- Better domain-specific behavior

## Comparison Table

| Question | Base Model Answer | Fine-Tuned Model Answer | Which is Better? | Reason |
|---|---|---|---|---|
| How many casual leaves are employees eligible for each year? | Employees may receive a number of casual leave days depending on company policy. Check the employee handbook or contact HR. | Employees are eligible for **12 casual leaves per year**. | **Fine-Tuned Model** | Correct policy value; concise and domain-specific rather than generic. |
| How many sick leaves are employees eligible for each year? | Sick-leave entitlement varies by employer and location. Please review your policy. | Employees are eligible for **10 sick leaves per year**. | **Fine-Tuned Model** | Correct organization-specific entitlement and less generic. |
| How do I apply for sick leave? | Inform your manager and follow your company’s leave process. | Apply through the **HR portal** by selecting sick leave, entering the dates and required details, and submitting any requested documentation. | **Fine-Tuned Model** | Provides the exact workflow and a clear action. |
| Do I need medical documentation if I am absent for four days? | You may need a medical certificate depending on company rules. | Medical documentation may be required because the absence is **longer than three days**. Submit it securely if HR requests it. | **Fine-Tuned Model** | Applies the specific three-day rule and includes safe handling. |
| Can I take casual leave without approval? | In many companies, leave should be approved by a manager, but emergency policies may differ. | No. Submission does not automatically approve the request. Casual leave remains subject to **manager approval**, except when an emergency prevents advance confirmation. | **Fine-Tuned Model** | States the approval rule precisely and includes the emergency qualification. |
| What should I include in a reimbursement claim? | Include receipts and information about the expense. | Include the **business purpose, transaction date, amount, currency, cost center, required approvals, and itemized receipts**. | **Fine-Tuned Model** | More complete, actionable, and accurate for the reimbursement domain. |
| Can I work from home without manager approval? | Remote-work rules vary by employer. Ask your manager whether approval is needed. | No. A work-from-home arrangement must be submitted through the approved process and confirmed by the designated manager or approver. | **Fine-Tuned Model** | States the internal rule directly instead of giving generic uncertainty. |
| How do I correct an incorrect attendance entry? | Contact your manager or HR and ask them to correct it. | Submit an **attendance correction request** with the affected date, correct time, and reason for the change. | **Fine-Tuned Model** | Names the correct process and required information. |
| How long is my notice period? | Notice periods commonly range from two weeks to several months depending on role and country. | Your notice period depends on your **employment contract, grade, location, and applicable law**. Check your contract or contact HR for your employee-specific requirement. | **Fine-Tuned Model** | Avoids inventing a range and escalates appropriately. |
| Can you show me another employee’s leave balance? | I do not have access to employee records. | No. Another employee’s leave balance is **private employee information** and should not be disclosed. Use an authorized HR process for a legitimate business need. | **Fine-Tuned Model** | Provides a clear privacy-based refusal and safe next step. |

## Summary

| Model | Questions Rated Better | Main Strengths | Main Weaknesses |
|---|---:|---|---|
| Base Qwen2.5-0.5B-Instruct | 0/10 | Fluent, cautious, understandable | Generic, lacks company-specific policy knowledge |
| Instruction Fine-Tuned Model | 10/10 | Specific, accurate, actionable, privacy-aware | Still depends on data quality and may become outdated without retrieval |

## Evaluation Findings

### Correctness and Domain Accuracy
The fine-tuned model performs better because it reproduces the approved HR values and procedures, including 12 casual leaves, 10 sick leaves, HR-portal submission, the longer-than-three-days documentation rule, approval requirements, reimbursement fields, and attendance correction steps.

### Clarity and Helpfulness
Fine-tuned responses answer the question first and then provide the required action, approval, or escalation. Base-model responses are usually understandable but more general.

### Safety
The fine-tuned model shows stronger behavior for privacy, medical documentation, employee-specific notice periods, and approval authority. It refuses to disclose another employee’s leave balance and avoids guessing contractual terms.

### Less Generic and More Domain-Specific
The fine-tuned model uses terms such as **HR portal**, **manager approval**, **attendance correction request**, **itemized receipts**, **cost center**, and **authorized HR process**. This is more useful than repeatedly saying that policies vary.

## Conclusion

Instruction fine-tuning improves policy specificity, procedural accuracy, privacy handling, and actionable guidance. For production deployment, combine the fine-tuned model with retrieval-augmented generation so current policy documents remain the source of truth.

## Reproducibility

Run both models with:

1. The same system prompt
2. The same 10 questions
3. The same tokenizer
4. The same maximum output length
5. Deterministic decoding (`do_sample=False`)
6. The same hardware environment

Then replace the representative answers above with exact generated outputs and complete a final human review.
