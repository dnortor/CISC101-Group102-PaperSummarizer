
---

# `/modules/03_guardrails.md`

```markdown
# Module 3: Guardrails

## Purpose
Enforce safety, quality, and evidence-based rules.

## Responsibilities
- Flag missing or empty sections.
- Warn about sections <50 words.
- Prevent hallucination: only use explicit paper content.
- Validate citations.
- Detect redundancy across sections.
- Enforce terminology in expert summaries.
- Handle long-paper chunking.
- Enforce 150-word limit per section.

## Safety Checks
- [ ] No invented citations
- [ ] No extrapolated results
- [ ] All claims traceable to source
- [ ] Terminology matches paper (expert mode)
- [ ] No redundancy between sections
- [ ] 150-word limit respected

## Integration Points
- Runs checks during **Module 2** processing.
- Passes warnings to **Module 4** for rendering.

## Example Output
```json
{
  "warnings": [
    "Section 'Conclusion' has only 40 words",
    "Redundancy detected between Abstract and Introduction"
  ]
}
