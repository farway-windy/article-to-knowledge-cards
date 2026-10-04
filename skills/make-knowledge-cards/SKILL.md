---
name: make-knowledge-cards
description: "Convert a pasted article or local Markdown/TXT file into 5-8 faithful, non-duplicative knowledge cards. Do not use for web scraping, PDFs, Anki exports, or GUI workflows."
---

# Make Knowledge Cards

Turn an article into concise cards for review. The goal is to preserve the genuinely important knowledge without adding or distorting information.

## Supported inputs

- Article text pasted directly by the user.
- A local `.md` or `.txt` file at a path supplied by the user.
- If the user supplies only a URL, do not fetch it. Explain that scraping is not supported and ask for the article text or a Markdown/TXT file.
- Do not handle PDFs, Anki exports, or GUI workflows.

## Workflow

1. Read the complete source. For a file, read the text directly and do not guess at missing content.
2. Find the thesis, key definitions, mechanisms, causal relationships, important distinctions, conditions, procedures, conclusions, and the key facts that support them.
3. Merge statements that repeat, entail, or merely restate the same knowledge point.
4. Rank the remaining points by importance. If there are more than eight central points, keep the eight most important; do not merge independent points merely to reach the limit.
5. Use 5-8 cards when the source supports them. If it supports fewer, output only the cards that are justified and add a short notice in the output language, such as: "Not enough source information; generated N cards." If the source has essentially nothing extractable, create no cards and say so.
6. Before writing, check each card for fidelity, single-point focus, and traceability back to the source.

## Card rules

- **One knowledge point per card.** Do not combine independent conclusions, procedures, or concepts. A tightly connected cause-and-effect or condition-and-conclusion pair can be one point.
- **Prioritize importance.** Keep central conclusions, definitions, mechanisms, distinctions, boundaries, actionable methods, and essential evidence. Omit greetings, repetition, promotion, irrelevant anecdotes, and minor details.
- **Do not invent.** Do not add background, numbers, dates, names, causes, consequences, recommendations, or cases that are absent from the source. Do not turn correlation into causation, possibility into certainty, or an opinion into a fact. Preserve qualifications and uncertainty.
- **Use only source-grounded examples.** When the source has a suitable example, use it in the Example field. Otherwise, write a self-test question whose answer follows directly from that card's core knowledge and explanation.
- **Be concise but complete.** State the core knowledge in 1-2 sentences. Use the explanation to clarify what it means, why it holds, or when it applies; do not merely repeat the source.
- **Make titles specific.** Use a short phrase that identifies the point. Avoid vague labels such as "Important concept" or "Other information."

## Output format

Write in the source language unless the user requests another language. Use this Markdown structure by default:

```markdown
# Knowledge Cards

## 1. Card title

- **Core knowledge**: One sentence stating one knowledge point.
- **Concise explanation**: Explain the point and its boundary or purpose.
- **Example**: The example from the source.

## 2. Next card

- **Core knowledge**: ...
- **Concise explanation**: ...
- **Self-test**: A question answerable from this card alone.
  - **Answer key**: The answer in one or two points.
```

For each card, use either `Example` or `Self-test`, not both. Use `Example` only when the source provides one. Do not split similar material just to reach five cards.