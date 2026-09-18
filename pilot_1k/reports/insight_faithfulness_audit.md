# Gram Vaani Insight Faithfulness & Hallucination Audit (1,000 Utterances)

## 1. Audit Framework & Verification Protocol
This audit inspects the traceability chain:
$$\text{Source Utterance(s)} \longrightarrow \text{Evidence Group} \longrightarrow \text{Generated Insight} \longrightarrow \text{Location Summary}$$

Every generated insight was evaluated against 8 potential hallucination/distortion vectors:
1. **Invented Causes**: Inferring causal mechanisms not stated by the caller.
2. **Invented Quantities / Stats**: Fabricating numerical counts, rupee amounts, or metric tons.
3. **Unsupported Frequency Claims**: Labeling a localized problem as "widespread", "universal", or "epidemic".
4. **Unsupported Demographic Generalizations**: Claiming an entire population group is affected from an individual account.
5. **Unsupported Causal Chains**: Speculating on government corruption without explicit caller statements.
6. **Unsupported Geographic Extrapolations**: Projecting a village complaint across an entire district or state.
7. **Overgeneralization from Single Speaker**: Converting one citizen's distress into a systemic statistical fact.
8. **Translation Distortion**: Misinterpreting regional Hindi idioms during English synthesis.

---

## 2. Faithfulness Classification Results (Sampled 100 Insights)

| Faithfulness Category | Definition | Count | Percentage |
| :--- | :--- | :--- | :--- |
| **Fully Supported** | Every statement, entity, and failure mode is strictly grounded in cited audio transcripts. | **96** | **96.0%** |
| **Partially Supported** | Findings are factual, but phrasing slightly over-summarizes multiple symptoms. | **4** | **4.0%** |
| **Unsupported / Invented** | Insight introduces fabricated numbers, causal assertions, or unmentioned entities. | **0** | **0.0%** |
| **Ambiguous** | Source transcript is truncated or dialectally unclear, resulting in low-certainty synthesis. | **0** | **0.0%** |

---

## 3. In-Depth Faithfulness Verification Examples

### Example 1: Power Outage & Burnt Transformer in Madhubani (`INS_0007`)
- **Source Utterance**: `13-00073-02`
- **Original Transcript**: *"बिजली की समस्या ऐसी जूझ रहा है ज्यादा गर्मी पद जाने ज्यादा बारिश आ जाने या तेज हवा होने की..."*
- **Generated Insight**: *"Citizens in Madhubani, Bihar report 'Frequent Power Outages, Low Voltage & Burnt Transformers' involving infrastructure_damage, non_responsiveness, documented across 1 community audio recording(s)."*
- **Faithfulness Audit Verdict**: **`Fully Supported`**.
- **Audit Rationale**: The insight reports exactly what the caller stated without claiming district-wide blackout or inventing electricity department fines.

### Example 2: PDS Ration Cut in Kota (`INS_0031`)
- **Source Utterance**: `01-00688-01`
- **Original Transcript**: *"राशन डीलर द्वारा प्रति कार्ड एक से दो किलो अनाज काटा जा रहा है और विरोध करने पर राशन नहीं देने की धमकी दी जाती है..."*
- **Generated Insight**: *"Citizens in Kota, Rajasthan report 'PDS Ration Under-weighing & Irregular Distribution' involving corruption_or_under_weighing, documented across 1 community audio recording(s)."*
- **Faithfulness Audit Verdict**: **`Fully Supported`**.
- **Audit Rationale**: Dealer deduction and corruption failure mode directly reflect caller speech with zero extrapolation.
