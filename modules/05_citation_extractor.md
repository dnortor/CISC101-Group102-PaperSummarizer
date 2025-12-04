
---

# `/modules/05_citation_extractor.md`

```markdown
# Module 5: Citation Extractor

## Purpose
Identify, extract, and organize citations from the paper.

## Responsibilities
- Scan paper for citation patterns ([Author, Year], numbered references).
- Extract referenced works with details.
- Link citations to sections.
- Create formatted reference list.
- Identify most frequently cited works.
- Track findings supported by citations.
- Generate citation statistics.

## Output
Structured list of references with section mapping.

## Integration Points
- Runs independently on full paper.
- Passes citation list to **Module 4**.

## Example Output
```json
{
  "citations": [
    {"section": "Abstract", "reference": "Vaswani et al., 2017"},
    {"section": "Results", "reference": "Bahdanau et al., 2015"}
  ],
  "stats": {
    "total_citations": 25,
    "citations_per_section": {"Abstract": 2, "Results": 10}
  }
}
