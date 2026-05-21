---
name: ljg-word
description: Deep-dive English word mastery tool. Deconstructs a single English word into core semantics and epiphany. Use when user asks to explain/master a specific English word.
version: "1.0.1"
user_invocable: true
---

## Usage

<example>
User: Deeply explain the word "Serendipity".
Assistant: [Calls ljg-explain-words with "Serendipity"]
</example>

## Instructions

The goal is not translation, but to help the user master the word's deep meaning and usage.

For the input `word` (convert to lowercase, capitalize first letter), perform the following analysis and output directly in Markdown within the conversation:

### Output Structure

#### 1. Title Line

```
## {Word}  /{phonetic}/  {Chinese translation}
```

#### 2. Core Semantics

- **Original scene**: Describe the word's most physical source image in one sentence (e.g., Incubate: a hen sitting on eggs).
- **Core imagery**: Extract a formula (e.g., warmth + time + protection = incubation).
- **Explanation**: Elaborate on its deep meaning and modern usage with insightful language. Clear paragraphs, **bold** key terms. Be penetrating -- show the intrinsic connections between etymology and cross-domain meanings.

#### 3. The One-Liner

A bilingual Chinese-English golden sentence, must have philosophical depth, summarizing the soul of the word. Use the quote format:

```
> "English sentence. Chinese golden sentence."
```
