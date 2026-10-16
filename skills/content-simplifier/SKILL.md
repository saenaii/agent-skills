---
name: content-simplifier
description: Simplify complex documents and rewrite drafts into clear, low-cognitive-load content that beginners can understand. Use when asked to summarize, explain, simplify, restructure, or improve documentation readability while preserving factual and technical accuracy.
---

# Content Simplifier

Reduce the cognitive load of documents so readers can quickly understand:

- What this is
- Why it matters
- How it works
- What they should do next

The goal is not merely to shorten the content. The goal is to make the meaning easier to understand without losing important facts, constraints, or technical precision.

## Mode Selection

Choose the mode based on the user's intent:

- **Input Simplification:** The user provides an existing document and wants to understand, summarize, or simplify it.
- **Output Rewriting:** The user provides a draft, proposal, explanation, or technical document and wants it rewritten for clarity.
- If the user asks to understand and rewrite the same document, complete Input Simplification first, then apply Output Rewriting.

Do not rewrite a document merely because it is technical. First determine what the user wants to achieve.

## General Principles

1. Preserve facts, constraints, terminology, and causal relationships.
2. Simplify the language without simplifying away important meaning.
3. Prefer short sentences, concrete verbs, and familiar words.
4. Explain a technical term the first time it appears.
5. Put the conclusion before supporting details.
6. Use one paragraph to express one main idea.
7. Use headings, lists, tables, and diagrams when they improve comprehension.
8. Use analogies only when they accurately clarify the concept.
9. Clearly distinguish facts, inferences, assumptions, and uncertainties.
10. Adapt the structure to the audience and purpose instead of applying a rigid template.

## Input Simplification Mode

When the user wants to understand an existing document, provide:

### 1. One-Sentence Summary

Explain the core message in one simple sentence.

### 2. TL;DR

Summarize in 3-7 points:

- What problem the document addresses
- Its main idea or mechanism
- Why it matters
- What the reader should remember

### 3. Logical Structure

Explain the document's actual reasoning:

1. Starting point: the problem, background, or goal
2. Main body: key concepts, steps, or decisions
3. Result: conclusion, impact, or next action

Do not merely repeat the document's table of contents. Explain how the parts relate to each other.

### 4. Key Concepts

Use a table when useful:

| Term | Simple Explanation | Role in the Document |
| --- | --- | --- |

### 5. Intuitive Explanation

Provide an analogy only when it improves understanding. Explain the limits of the analogy when it could be misunderstood.

### 6. Key Takeaways

List the 3-5 most important things the reader should remember.

For long documents, optionally identify:

- Sections that can be skipped initially
- Sections that deserve deeper reading
- Questions or claims that need verification

## Output Rewriting Mode

When the user wants a document rewritten for clarity:

### 1. Identify the Audience and Goal

Use the audience and context provided by the user.

If they are not provided:

- Assume the reader has basic background knowledge but is unfamiliar with this specific topic.
- Assume the goal is for the reader to understand the subject and take the next appropriate action.

Ask a question only when missing information would materially change the document.

### 2. Restructure the Content

Prefer this order when appropriate:

1. Conclusion or objective
2. Why it matters
3. Key concepts
4. How it works or what to do
5. Example
6. Limitations and caveats
7. Next steps

Adjust the structure to fit the content. Do not add sections that do not serve a clear purpose.

### 3. Simplify the Language

Look for opportunities to:

- Remove unnecessary background and repetition
- Replace abstract nouns with concrete actions
- Split long sentences
- Replace passive voice with active voice
- Replace unnecessary jargon with familiar language
- Explain terminology that cannot be replaced
- Make implicit relationships explicit

### 4. Improve Visual Structure

Choose the format that best supports comprehension:

- Use numbered lists for procedures
- Use bullet lists for parallel items
- Use tables for comparisons
- Use decision structures for conditions and outcomes
- Use arrows or stages for processes
- Put important conclusions near the beginning

Do not add headings or lists merely to make the document look structured.

### 5. Perform a Beginner Review

Check whether:

- The opening explains the topic and conclusion
- The reader understands the purpose of the document
- Necessary technical terms are explained
- The reader knows what to do next
- The reasoning contains unexplained jumps
- Any sentence is too long or expresses multiple independent ideas
- Important limitations were accidentally removed
- Assumptions or guesses are presented as facts

If background knowledge is still required, add a short "Before you start" section.

## Output Requirements

By default, provide the rewritten or simplified document directly.

If the user asks for an explanation of the changes, also summarize:

- What was removed
- What was reorganized
- Which terms were simplified or explained
- Which complex expressions were retained for accuracy

Do not provide only editing suggestions when the user expects a usable document.

## Quality Standard

The final content should satisfy these conditions:

- The reader understands the topic and conclusion early
- Facts, assumptions, inferences, and uncertainties are distinguishable
- The reader does not need to repeatedly reread the main argument
- The reader knows what to do next
- Clarity is improved without sacrificing accuracy
- The structure supports understanding rather than decoration
