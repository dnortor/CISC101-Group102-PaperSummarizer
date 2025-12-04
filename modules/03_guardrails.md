
# Module 03: Guardrails

## Change Log
**Date**: Thurs dec 4th  
**Changes**: 
1. Added evidence_mode variable with "strict" setting to enforce evidence-based summaries
2. Implemented standardized warning messages for missing, empty, or short (<50 words) sections

---

## Purpose
Enforce safety, quality, and evidence-based rules throughout the summarization process.

## Variables

### evidence_mode
- **Type**: String
- **Values**: "standard" | "strict"
- **Default**: "standard"
- **Description**: Controls how strictly the system adheres to source material

## Guardrail Rules

### 1. Strict Evidence Mode

**WHEN evidence_mode = "strict":**

**Rules:**
- Only include claims, equations, results, and statements that explicitly appear in the provided paper text
- Do not infer, extrapolate, or fill in gaps with general knowledge
- Do not paraphrase in ways that add information not present in the source
- If a section lacks sufficient detail for summarization, explicitly state this

**Behavior:**
- Before generating any summary content, verify each statement against source text
- If information is insufficient:
  ```
  "The source text does not provide enough detail to summarize this section in strict evidence mode."
  ```
- If a section contains partial information:
  ```
  "Limited information available. Summary based only on explicitly stated content: [summary]"
  ```
- Track all claims back to specific paper content
- Reject any LLM-generated elaboration or background knowledge

### 2. Section Warning Messages

**Missing or Empty Sections:**

WHEN a requested section:
- Is not found in the paper, OR
- Contains no text content, OR
- Is present but empty

**Output standardized warning:**
```
Section skipped: No usable text was provided for "[Section Name]".
```

**Short Sections (< 50 words):**

WHEN a section contains fewer than 50 words:

**Output standardized warning:**
```
 Section very short: "[Section Name]" contains fewer than 50 words. Summary may be incomplete or lack detail.
```

**Additional context to include:**
- Word count: "[X] words found"
- Option: "Consider this a preliminary or partial section."

### 3. Hallucination Prevention

**Always Active (regardless of evidence_mode):**

- Cross-reference all technical terms against paper content
- Never invent:
  * Citations or references
  * Equations or formulas
  * Results or statistics
  * Author claims or conclusions
- If uncertain about content presence, flag for review
- Maintain explicit boundaries between:
  * Content from the paper
  * General domain knowledge (not allowed in summaries)

### 4. Long Paper Chunking

**WHEN paper exceeds context window limits:**

**Strategy:**
1. Split paper into logical chunks (by section or page range)
2. Process each chunk separately
3. Track which sections appear in which chunks
4. Merge results carefully to avoid duplication
5. Flag any sections that span multiple chunks

**Warning for chunked processing:**
```
 Note: This paper was processed in multiple segments. Summaries are based on complete available content.
```

### 5. Content Quality Checks

**For each generated summary, verify:**
-  No invented citations
- No extrapolated results
-  No general knowledge filler
-  All claims traceable to source
-  Appropriate caveats for limited information

## Warning Output Format

All warnings should be collected and presented in the "Checks & Warnings" section of the final output:

```markdown
## Checks & Warnings

### Missing Sections
- Section skipped: No usable text was provided for "Future Work".

### Short Sections
- Section very short: "Conclusion" contains fewer than 50 words (42 words found). Summary may be incomplete or lack detail.

### Evidence Mode
- Strict evidence mode: Active. All summaries limited to explicitly stated content only.
```

## Integration Points
- **Receives from Module 02**: Section content and preliminary summaries
- **Validates**: All content before passing to Module 04
- **Flags**: Issues to be included in final output warnings
}
