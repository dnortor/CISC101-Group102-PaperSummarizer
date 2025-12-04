
---

# `/modules/06_key_contributions.md`

```markdown
# Module 6: Key Contributions Summarizer

## Purpose
Identify and highlight the paper's novel contributions.

## Responsibilities
- Scan for explicit claims of novelty.
- Extract methodological innovations.
- Highlight main experimental results.
- Identify performance improvements over baselines.
- Summarize main claims.
- Present contributions in bullet format.
- Compare with prior work.

## Output
Bullet list of 3–7 key contributions with evidence.

## Integration Points
- Runs independently on full paper.
- Passes contributions to **Module 4**.

## Example Output
```markdown
## Key Contributions
- Introduced Transformer architecture based solely on attention [Vaswani et al., 2017].
- Eliminated recurrence, enabling parallelization and faster training.
- Achieved state-of-the-art results in translation benchmarks.
- Demonstrated scalability with large