[01_intake_setup.md](https://github.com/user-attachments/files/23943751/01_intake_setup.md)
# Module 1: Intake & Setup

## Purpose
Initialize and validate all inputs before processing the paper.

## Responsibilities
- Parse paper content (PDF or text).
- Normalize section names (e.g., "Introduction" vs "1. Introduction").
- Detect missing sections requested by user.
- Identify sections with insufficient content (<50 words).
- Store target audience preference (Expert/Novice).
- Set up processing variables.
- Create section inventory with word counts.

## Variables
- `target_audience`: "expert" | "novice"
- `section_list`: array of requested sections
- `paper_content`: full text of paper
- `section_inventory`: map of {section_name: {exists: bool, word_count: int}}

## Logic Flow
1. Parse input PDF/text.
2. Normalize section names.
3. Build `section_inventory` with existence and word counts.
4. Flag missing or short sections.
5. Store `target_audience`.

## Integration Points
- Provides validated inputs to **Module 2 (Section Loop)**.
- Supplies section inventory for guardrails in **Module 3**.

## Example Input
- Paper: "Attention Is All You Need"
- Sections: ["Abstract", "Introduction", "Model Architecture", "Results", "Conclusion"]
- Audience: "Expert"

## Example Output
```json
{
  "target_audience": "expert",
  "section_list": ["Abstract", "Introduction", "Model Architecture", "Results", "Conclusion"],
  "section_inventory": {
    "Abstract": {"exists": true, "word_count": 120},
    "Introduction": {"exists": true, "word_count": 500},
    "Model Architecture": {"exists": true, "word_count": 800},
    "Results": {"exists": true, "word_count": 600},
    "Conclusion": {"exists": true, "word_count": 200}
  }
}
