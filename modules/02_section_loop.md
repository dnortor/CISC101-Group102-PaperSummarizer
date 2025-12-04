
---

# `/modules/02_section_loop.md`

```markdown
# Module 2: Section Loop

## Purpose
Process each section iteratively and generate structured summaries.

## Responsibilities
- Iterate through each requested section in paper order.
- Extract relevant content for each section.
- Generate ≤150-word summary.
- Identify and cite key findings.
- Check redundancy with previous sections.
- Ensure terminology matches source (expert mode).
- Store summaries in structured format.
- Track citations used.

## Logic Flow

FOR each section in section_list (in paper order):
Extract section content from paper
Identify key findings and claims
Generate 150-word summary with citations
Check for redundancy with previous summaries
Validate terminology matches source
Store summary with metadata

## Integration Points
- Receives validated inputs from **Module 1**.
- Runs safety checks via **Module 3**.
- Passes structured summaries to **Module 4**.

## Example Output
```json
{
  "section": "Abstract",
  "summary": "This paper introduces the Transformer architecture, which relies entirely on attention mechanisms... [Vaswani et al., 2017]",
  "citations": ["Vaswani et al., 2017"]
}
