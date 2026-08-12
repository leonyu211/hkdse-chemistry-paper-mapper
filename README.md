# HKDSE Chemistry Toolkit

A Codex skill for two HKDSE Chemistry workflows:

- Mapping assessment-paper questions to HKDSE chapters and topics
- Generating syllabus-aligned extra-exercise worksheets with separate mark schemes as HTML or Unicode pure text

The skill never creates DOCX or PDF output. Uploaded Word files may be analysed as inputs only.

## Use

Invoke the skill:

```text
Use $hkdse-chemistry-paper-mapper.
```

The skill will ask which mode to use when your request is ambiguous.

For paper mapping, upload or provide:

- The chemistry question paper
- Optionally, a syllabus/chapter map

Example:

```text
Use $hkdse-chemistry-paper-mapper to analyse this chemistry paper and map every question to HKDSE chapters and topics.
```

For worksheet generation, ask for a chapter/topic:

```text
Use $hkdse-chemistry-paper-mapper to generate extra exercises for Chapter 30: Redox Reactions.
```

The skill includes a built-in HKDSE chapter map and falls back to it when no separate syllabus file is supplied.
