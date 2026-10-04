# Make Knowledge Cards

`make-knowledge-cards` is a Codex skill for turning reading material into compact, reviewable knowledge cards.

## 1. What Problem It Solves

Long articles often contain a few important ideas mixed with repetition, examples, qualifications, and less important details. Manually extracting those ideas can take time, while automatic summaries can introduce facts that were not in the source.

This skill solves that problem by:

- Extracting only the important, source-grounded knowledge.
- Keeping one knowledge point per card.
- Removing repeated or overlapping material.
- Avoiding invented background, examples, numbers, or conclusions.
- Returning fewer than five cards when the article does not contain enough distinct knowledge, instead of padding the output.

By default, the output is Markdown returned in the conversation. The skill itself does not include scripts for creating or modifying files.

## 2. Main Features

- Accepts article text pasted directly by the user.
- Accepts local `.md` and `.txt` files.
- Targets 5-8 cards when the source supports that many distinct points.
- Returns only the justified cards when the source contains less information.
- Gives each card a specific title, one core knowledge point, a concise explanation, and either an example or a self-test question with an answer key.
- Uses examples only when they appear in the source.
- Preserves qualifications and uncertainty from the original text.
- Writes in the source language unless the user requests another language.
- Removes semantic duplicates before selecting the most important points.

Not supported: web scraping, PDF files, Anki export, and graphical interfaces.

## 3. Installation

The skill has no scripts or runtime dependencies. Install it by copying the skill directory into a Codex skills directory.

### Windows PowerShell

```powershell
New-Item -ItemType Directory -Force "$HOME\.codex\skills" | Out-Null
Copy-Item -Recurse -Force ".\skills\make-knowledge-cards" "$HOME\.codex\skills\"
```

### macOS or Linux

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R skills/make-knowledge-cards "${CODEX_HOME:-$HOME/.codex}/skills/"
```

If the project is already inside a discoverable Codex skills directory, no copy is required.

## 4. Usage

### Paste an Article

```text
Use $make-knowledge-cards to turn the following article into knowledge cards.

[Paste the article here.]
```

### Use a Local Markdown or TXT File

```text
Use $make-knowledge-cards to read ./notes/article.md and turn it into knowledge cards.
```

You can also provide a `.txt` path. If you provide only a URL, the skill will not fetch it; paste the article text or provide a local Markdown/TXT file instead.

## 5. Input and Output Example

### Input

```text
Spaced repetition means reviewing material across multiple sessions instead of cramming. Retrieval practice means recalling information without looking at it. A difficult but successful recall strengthens memory more than rereading. If recall fails completely, review the material before trying again.
```

### Output

```markdown
Not enough source information; generated 3 cards.

# Knowledge Cards

## 1. Spacing Beats Cramming at Equal Study Time

- **Core knowledge**: Reviewing material across multiple sessions is preferable to cramming.
- **Concise explanation**: Spacing the reviews distributes the same learning over time rather than concentrating it in one session.
- **Self-test**: How does spaced repetition differ from cramming?
  - **Answer key**: Spaced repetition uses multiple sessions instead of one concentrated session.

## 2. Retrieval Means Recalling Without Looking

- **Core knowledge**: Retrieval practice requires producing information from memory rather than viewing it.
- **Concise explanation**: The act of recall is what distinguishes retrieval practice from rereading.
- **Self-test**: What must a learner do during retrieval practice?
  - **Answer key**: Recall the information without looking at it.

## 3. Successful Difficulty Strengthens Memory

- **Core knowledge**: A difficult but successful recall strengthens memory more than rereading.
- **Concise explanation**: The benefit depends on success; complete failure requires reviewing the material before another attempt.
- **Self-test**: What should happen after a complete recall failure?
  - **Answer key**: Review the material before trying to recall it again.
```

The example is intentionally shorter than five cards. It demonstrates the required behavior when the source does not contain enough distinct knowledge points.

## Project Structure

```text
skills/
`-- make-knowledge-cards/
    |-- SKILL.md
    `-- agents/
        `-- openai.yaml
```

## Validation

When the `skill-creator` tooling is available, run:

```bash
python /path/to/skill-creator/scripts/quick_validate.py skills/make-knowledge-cards
```

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
