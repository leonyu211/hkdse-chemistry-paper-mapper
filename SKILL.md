---
name: "hkdse-chemistry-paper-mapper"
description: "Analyse an HKDSE or senior-secondary chemistry question paper and produce a question-by-question table mapping each MCQ and structured question to HKDSE Chemistry chapters, syllabus topics, and assessed concepts. Use when a user provides a chemistry paper plus an HKDSE syllabus/chapter map and asks for topic coverage, chapter analysis, paper blueprinting, or assessment mapping."
---

# HKDSE Chemistry Paper Mapper

Use this skill to analyse a senior-secondary / HKDSE Chemistry assessment paper and map every question to the supplied HKDSE Chemistry syllabus chapters and topics.

## Inputs

Expect one or both of:

- A question paper, commonly `.docx`, `.pdf`, image pages, or pasted text.
- A syllabus/chapter map supplied by the user. Treat it as authoritative for chapter names, topic names, branch labels, and scope.

If no syllabus/chapter map is supplied, ask the user to provide one before doing final mapping. Do not invent chapter titles.

## Workflow

1. Extract the paper content.
   - For `.docx`, use a document text extractor and, when diagrams/tables matter, render pages or inspect images.
   - Preserve section labels such as Paper 1A, Paper 1B, MCQ, structured questions, question numbers, marks, and table labels.
   - Note where graphs, structural formulae, or diagrams are embedded and may not appear in plain text.

2. Extract the syllabus taxonomy.
   - Identify official HKDSE topic number/name, chapter number/title, branch, and scope bullets.
   - Use the supplied chapter map as the naming authority.
   - If chapter ranges have no individual titles, keep the range label and do not create unofficial titles.

3. Classify each question.
   - Assign the dominant chapter first.
   - Add secondary chapters where a question genuinely combines topics, such as organic synthesis plus isomerism, or thermochemistry plus acid strength.
   - Use concise concept labels, not just broad chapter names.
   - For diagram-dependent questions, infer only from visible wording/options and flag uncertainty briefly.

4. Produce the output.
   - Separate MCQs and structured questions.
   - Use Markdown tables.
   - Include an overall coverage summary showing dominant topics and notable cross-topic links.

## Output Format

Start with a one-paragraph note describing the sources used and any extraction limitations.

Then provide:

```markdown
**Paper 1A MCQ Mapping**

| Q | Main HKDSE chapter(s) | Topic area assessed |
|---:|---|---|
| 1 | Ch. X Chapter Title | Concise concept description |

**Paper 1B Structured Question Mapping**

| Q | Main HKDSE chapter(s) | Topic area assessed |
|---:|---|---|
| 1 | Ch. X Chapter Title | Concise concept description |

**Overall Pattern**

[Short summary of the main weighting, recurring chapters, and notable gaps.]
```

## Classification Heuristics

- Atomic structure, isotopes, electron arrangement: Topic II, Ch. 5.
- Periodic table trends, group properties, flame tests: Topic II, Ch. 6, or Topic XII if advanced periodic patterns are assessed.
- Bonding and structure: Topic II, Ch. 7-9; use Ch. 26 for intermolecular forces.
- Metal reactions, reactivity series, extraction, corrosion: Topic III, Ch. 10-13.
- Acids, bases, concentration, pH, salts, titration: Topic IV, Ch. 14-19.
- Fossil fuels, alkanes, alkenes, cracking, addition polymerisation basics: Topic V, Ch. 20-23.
- Redox, oxidation numbers, electrolysis, cells: Topic VII, Ch. 28-32.
- Enthalpy, calorimetry, Hess cycles, bond enthalpy: Topic VIII, Ch. 33-35.
- Rates, rate graphs, collision theory, catalysts, gas volume: Topic IX, Ch. 36-38.
- Equilibrium, Kc, Le Chatelier: Topic X, Ch. 39-41.
- Organic functional groups, isomerism, synthesis, identification, aspirin, detergents, nylon/polyesters: Topic XI, Ch. 42-46.
- Period 2/3 and transition-metal properties: Topic XII, Ch. 47-49.
- Industrial rate equations, activation energy, catalysis, green chemistry: Topic XIII, Ch. 50-55.
- Materials, polymeric materials, alloys, nanomaterials, biodegradable plastics: Topic XIV, Ch. 56-60.
- Chemical tests, separations, quantitative analysis, instrumental analysis: Topic XV, Ch. 61-65.

## Quality Checks

- Confirm the counted number of MCQs and structured questions matches the paper instructions.
- Check that every question number appears exactly once in the mapping.
- Use the user's syllabus wording for chapter names.
- Keep uncertainty local: mark only the affected question as "diagram-dependent" instead of weakening the whole analysis.
- Do not provide answer keys unless the user asks.
