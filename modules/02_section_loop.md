
# Module 02: Section Loop

## Change Log
**Date**: [Thurs Dec 4th]  
**Changes**: Added summary_level variable with conditional logic for "short" and "detailed" summary modes. Detailed mode now includes both paragraph summary and bullet list of key points.

---

## Purpose
Process each requested section iteratively and generate appropriate summaries based on the specified detail level.

## Variables

### summary_level
- **Type**: String
- **Values**: "short" | "detailed"
- **Default**: "short"
- **Description**: Controls the depth and format of section summaries

## Process Flow

### For Each Section in Section List:

1. **Extract Content**
   - Locate the section in the provided paper text
   - Extract all content between section headers
   - Store raw content for processing

2. **Content Validation**
   - Check if section exists (non-empty)
   - Count words in section
   - Flag to Module 03 (Guardrails) if issues detected

3. **Generate Summary Based on Level**

   **IF summary_level = "short":**
   - Generate a concise 1-2 sentence summary
   - Focus on the main point or finding
   - Use clear, direct language
   - Format: Plain paragraph text
   
   **IF summary_level = "detailed":**
   - Generate a short paragraph (3-5 sentences) covering:
     * Main topic or purpose of the section
     * Key methodology or approach (if applicable)
     * Primary findings or arguments
   - THEN generate a bullet list with 3-5 key points:
     * Each point should be a specific detail or insight
     * Points should complement, not repeat, the paragraph
     * Use parallel structure for consistency
   - Format example:
     ```
     [Paragraph summary here...]
     
     Key Points:
     - [Point 1]
     - [Point 2]
     - [Point 3]
     - [Point 4]
     - [Point 5]
     ```

4. **Quality Check**
   - Ensure summary uses only content from the paper
   - Verify no hallucinated information
   - Confirm appropriate length constraints

5. **Store Summary**
   - Add section name and summary to output structure
   - Maintain order of requested sections
   - Tag with audience level for later rendering

## Output Format

Each processed section produces:
```
{
  "section_name": string,
  "summary": string,
  "detail_level": "short" | "detailed",
  "word_count": number,
  "warnings": array
}
```

## Integration Points
- **Receives from Module 01**: Normalized section list, paper content
- **Sends to Module 03**: Section content for guardrail checks
- **Sends to Module 04**: Completed summaries for rendering
  "section": "Abstract",
  "summary": "This paper introduces the Transformer architecture, which relies entirely on attention mechanisms... [Vaswani et al., 2017]",
  "citations": ["Vaswani et al., 2017"]
}
