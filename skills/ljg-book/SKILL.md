---
name: ljg-book
description: Dissect a book. Calm, concise, sharp, direct. Five moves to clarify: what question the author is answering, what unproven ground they stand on, what framework they use to see, what conclusions they reach, and a God's-eye compression of the entire book. Use when user says '拆书', '拆这本', '分析这本书', '这本书在讲什么', '上帝之眼看这本书', '压缩一本书', 'book', or shares a book name wanting structural analysis. NOT FOR chapter summaries (use Fabric extract_wisdom), papers (use ljg-paper), single-idea deep dives (use ljg-think), or domain rank reduction (use ljg-rank).
user_invocable: true
---

# ljg-book: Book Dissection

Input a book, output its skeleton.

## What Book Dissection Is

Not a review, not a chapter summary, not praise — it's extracting the author's skeleton and laying it on the table.

Reading a book, you easily get lost in the author's brushwork. Dissecting a book means jumping out of the brushwork to see the author's viewfinder. Once you see the viewfinder clearly, you see the whole book.

## The Five Moves

Ask each one separately. Then thread them together.

### 1. Core Question

What is the author really answering? This is a question, not a topic.

A topic is "free will" — a question is "Does free will actually exist, or do we just think we have it when we don't?"

Topic is a topic. Question is a question.

The question must be sharp — it's what was itching at the author before they wrote the entire book. The book is the answer, the question is the itch.

How to find it: read the author's introduction/preface, find the sentence "I wrote this book to…". If you can't find it, look at what the author keeps circling back to — the thing they can't shake off across hundreds of pages, that is the question itself.

### 2. Foundational Assumptions

What unproven ground does the author stand on?

Every book has several ceilings — things the author doesn't prove, they lean on them. Shake any one, and the whole book collapses.

Two operational questions to ask the book:
- What in this book is not allowed to be questioned? (Ask it and the author dismisses you as a layperson)
- What must the author believe to keep writing? (Without it, all subsequent arguments lose their pivot)

The answers are the book's foundational assumptions.

State them, don't elaborate. These are self-evident — lay them on the table. Proving or disproving them is not the dissector's job.

### 3. Analytical Framework

What lens does the author use to see the world?

Every author has a viewfinder. Darwin's viewfinder is "variation + selection + time" — he sees butterflies, people, tribes all through this frame. Marx's viewfinder is "relations of production determine superstructure" — he sees history, society, art all through this frame. Freud's viewfinder is "consciousness is the tip of the iceberg, what's underwater is the real protagonist" — he sees dreams, slips of the tongue, politics all through this frame.

To find the author's frame: what tool do they use repeatedly? What angle do they enter from? When they see X, their first reflex is to think of Y — that Y is their frame.

A frame isn't necessarily a noun. It can be an action ("reduce to root cause"), a distinction ("natural state vs. cultural state"), a contrast ("explicit logic vs. implicit structure").

Finding the frame requires ruthlessness — capture it in one sentence, not a chapter.

### 4. Core Arguments / Conclusions

What did the author ultimately conclude?

Not "how many examples did they give," not "how many steps in their argument." It's: close the book, what does the author want you to walk away with?

Often just one or two sentences.

Test: pull this sentence out, strip it of the author's context — does it still have force? If it just restates the book title, it's not a core argument — it's a label. If it's a platitude ("things are dialectical," "everything is connected"), it's empty.

Core arguments must be sharp — they can stand, they can be refuted, they can be cited.

No softness. "The author believes human nature is complex" is a soft statement — what isn't complex?

### 5. God's-Eye Compression

The whole book, hundreds of pages, seen from God's eye — compressed into a few sentences, what is it?

Not an abstract — an abstract is the author's own product description. God's-eye compression is you standing above the author looking down: what is the author actually saying.

Three to five sentences is enough. Each sentence must carry a load-bearing beam — one for foundational assumptions, one for the analytical framework, one for core arguments, plus one or two landing on reality.

After writing, silently ask: can someone who has never read this book, after reading these few sentences, roughly say they know what this book is about? Yes → pass.

## How to Write

Calm, concise, sharp, direct.

Don't praise the author, don't disparage the author, don't defend the author, don't apologize for the author.

Five sections, numbered 1-5. Within each section, write in one breath, no detours.

Each section opens with one anchoring sentence — the core of what this section says. Then expand with two or three sentences to make it clear. Don't list bullets endlessly — one prose paragraph beats ten bullets.

Short sentences. Cut prepositions. "Through / by means of / via / upon" — avoid whenever possible.

Plain English. Write like you speak. After finishing each section, read it aloud — anywhere it stumbles, rewrite the whole sentence (don't just swap words).

No academic tone. "The author argues that," "the author believes" — use sparingly. Say directly what the author did. "X points out in chapter N…" — kill all of these.

## How to Find Material

If the user only gives a book title —
- First WebSearch / WebFetch for author, introduction, table of contents, secondary interpretations of core arguments
- Answer only after obtaining the core argument
- Don't dissect from impression — impression-based dissection produces Wikipedia-style empty words

If the user provides a PDF / arxiv link / content — read directly, no need to search.

For classic books — LLM internal knowledge is acceptable, but silently ask: is what I'm saying actually in the book, or did I make it up? If made up, delete it.

## Output

1. Get timestamp: `date +%Y%m%dT%H%M%S` and `date "+%Y-%m-%d %a %H:%M"`
2. Write to `~/Documents/notes/{timestamp}--book-dissection-{book_title}__book.org`
3. org-mode format (headings with `*`, bold with `*bold*` single asterisks, no markdown double asterisks)
4. File header:

```
#+TITLE: Book Dissection: {Book Title}
#+SUBTITLE: {Author} | {one-sentence core argument}
#+DATE: [{YYYY-MM-DD Day HH:MM}]
#+FILETAGS: :book:{book domain e.g. philosophy/biology/economics}:
#+IDENTIFIER: {YYYYMMDDTHHMMSS}
```

5. Body: five sections, numbered 1-5, each in prose.
6. Report the file path to the user.

## Red Lines (must pass every one)

1. **No praise, no disparagement, no defense** — the dissector stands above the author, not as fan or opponent
2. **Calm, concise, sharp, direct** — read each section aloud, no stumbling
3. **Core argument must not be soft** — soft statements ("X is complex") die
4. **Foundational assumptions are stated, not argued** — just lay them out
5. **God's-eye compression ≤ 5 sentences** — one load-bearing beam per sentence
6. **Zero academic tone** — "the author argues / believes / points out" — use sparingly
7. **No translation-ese** — clear, plain English; read it aloud and ask: would a sharp writer write this way?
