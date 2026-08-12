---
name: "hkdse-chemistry-paper-mapper"
description: "Analyse HKDSE or senior-secondary chemistry question papers by mapping questions to chapters/topics, or generate HKDSE Chemistry extra-exercise worksheets with mark schemes as self-contained HTML or Unicode plain text. Use when a user asks for chemistry paper topic coverage, chapter analysis, assessment blueprinting, or syllabus-aligned worksheet generation. Never generate DOCX or PDF output."
---

# HKDSE Chemistry Paper Mapper and Worksheet Generator

Use this skill for two related HKDSE Chemistry tasks:

1. **Paper Mapping**: analyse a senior-secondary / HKDSE Chemistry assessment paper and map every question to HKDSE Chemistry syllabus chapters and topics.
2. **Worksheet Generation**: create syllabus-aligned extra exercises and a separate mark scheme for a selected HKDSE Chemistry chapter or topic.

## Hard Output Boundary

- Never create, convert to, attach, offer, or recommend `.docx`, Microsoft Word, or PDF output in either mode.
- Treat an uploaded `.docx` only as an input source to read or analyse. Its format does not determine the output format.
- Do not invoke document-generation or Word-export tools. A document-reading tool may be used only to extract content from an uploaded question paper.
- Return Paper Mapping results directly in the conversation as Markdown tables unless the user explicitly asks for one of the supported worksheet formats.
- For Worksheet Generation, the only permitted outputs are two self-contained `.html` files or Unicode pure text returned directly in the conversation, as defined in [references/worksheet-generation.md](references/worksheet-generation.md).
- If the user requests DOCX or PDF output, state briefly that this skill supports only HTML or Unicode pure text and ask them to choose one of those two modes. Do not silently substitute a Word file.

## Mode Selection

At the start of an ambiguous invocation, ask:

"Which mode would you like to use?

1. Paper Mapping - analyse a question paper and map each question to HKDSE chapters/topics.
2. Worksheet Generation - create extra exercises and a mark scheme as HTML or Unicode pure text for a selected HKDSE Chemistry chapter/topic."

Stop and wait for the user's choice.

If the user clearly asks to analyse, map, classify, blueprint, or review a paper, use Paper Mapping without asking.

If the user clearly asks to create, generate, practise, make exercises, worksheets, or mark schemes, use Worksheet Generation without asking. For worksheet generation, read [references/worksheet-generation.md](references/worksheet-generation.md) before asking follow-up questions or producing the exercise.

## Inputs

Expect:

- A question paper, commonly `.docx`, `.pdf`, image pages, or pasted text.
- Optionally, a syllabus/chapter map supplied by the user.

Use a user-supplied syllabus/chapter map as authoritative when it conflicts with the built-in reference below. If no syllabus/chapter map is supplied, use the built-in reference chapter map. Do not invent chapter titles.

## Paper Mapping Workflow

1. Extract the paper content.
   - For `.docx`, use a document text extractor and, when diagrams/tables matter, render pages or inspect images.
   - Preserve section labels such as Paper 1A, Paper 1B, MCQ, structured questions, question numbers, marks, and table labels.
   - Note where graphs, structural formulae, or diagrams are embedded and may not appear in plain text.

2. Extract the syllabus taxonomy.
   - Identify official HKDSE topic number/name, chapter number/title, branch, and scope bullets.
   - Use the supplied chapter map as the naming authority when present; otherwise use the built-in reference chapter map.
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
   - Return the analysis in the conversation. Do not package it as a DOCX or PDF.

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

## Reference Chapter Map

Use this map as the fallback chapter taxonomy when the user does not provide a separate syllabus/chapter map.

### Topic I - Planet Earth

Chapters 1-4: Individual titles not provided

Branch: Inorganic Chemistry

Scope:
- Atmosphere, ocean, rocks and minerals
- Elements, compounds and mixtures
- Physical and chemical changes
- Separation methods
- Solutions and crystallisation
- Word equations
- Tests for selected chemical species
- Extraction of useful materials
- Calcium carbonate and related reactions

Do not invent titles for Chapters 1-4.

### Topic II - Microscopic World I

Chapter 5: Atomic Structure

Chapter 6: Periodic Table

Chapter 7: Ionic and Metallic Bonding

Chapter 8: Covalent Bonding

Chapter 9: Structure and Properties

Branches:
- Inorganic Chemistry
- Structural Chemistry

Scope:
- Atomic structure and isotopes
- Electronic arrangements
- Periodic Table organisation and trends
- Ionic, covalent and metallic bonding
- Chemical formulae
- Relationships between structures, properties and uses

### Topic III - Metals

Chapter 10: Extraction of Metals

Chapter 11: Metal Reactivity

Chapter 12: Reacting Masses

Chapter 13: Corrosion Prevention

Branch: Inorganic Chemistry

Scope:
- Metal extraction
- Reactivity series
- Metal reactions
- Displacement reactions
- Chemical and ionic equations
- Mole calculations
- Reacting masses
- Empirical formulae
- Corrosion and prevention

### Topic IV - Acids and Bases

Chapter 14: Acids and Bases

Chapter 15: Concentrations

Chapter 16: Indicators

Chapter 17: Strength of Acids

Chapter 18: Salt Preparation

Chapter 19: Titrations

Branch: Inorganic Chemistry

Scope:
- Properties and reactions of acids and alkalis
- pH and indicators
- Strong and weak acids
- Molar concentration
- Neutralisation
- Salt preparation
- Standard solutions
- Acid-base titrations
- Volumetric calculations

### Topic V - Fossil Fuels and Carbon Compounds

Chapter 20: Fossil Fuels

Chapter 21: Homologous Series

Chapter 22: Alkanes and Alkenes

Chapter 23: Addition Polymers

Branch: Organic Chemistry

Scope:
- Petroleum fractions
- Environmental effects of fossil fuels
- Homologous series
- Formulae and systematic names
- Alkanes and alkenes
- Combustion, substitution, cracking and addition
- Addition polymerisation

### Topic VI - Microscopic World II

Chapter 24: Molecular Shapes

Chapter 25: Polarity

Chapter 26: Intermolecular Forces

Chapter 27: Ice

Branch: Structural Chemistry

Scope:
- Electronegativity
- Bond and molecular polarity
- Molecular shapes
- Van der Waals' forces
- Hydrogen bonding
- Structure and properties of ice
- Selected non-octet molecules

### Topic VII - Redox Reactions, Chemical Cells and Electrolysis

Chapter 28: Introduction to Chemical Cells

Chapter 29: Simple Chemical Cells

Chapter 30: Redox Reactions

Chapter 31: Advanced Concepts in Simple Chemical Cells

Chapter 32: Electrolysis

Branch: Physical Chemistry

Scope:
- Oxidation and reduction
- Oxidation numbers
- Oxidising and reducing agents
- Redox equations
- Chemical cells
- Electrode reactions
- Electrochemical series
- Electrolysis
- Preferential discharge

### Topic VIII - Chemical Reactions and Energy

Chapter 33: Introduction to Thermodynamics

Chapter 34: Typical Enthalpy Changes

Chapter 35: Hess's Cycle

Branch: Physical Chemistry

Scope:
- Conservation of energy
- Exothermic and endothermic reactions
- Enthalpy changes
- Calorimetry
- Standard enthalpy changes
- Hess's law
- Enthalpy cycles and calculations

### Topic IX - Rate of Reaction

Chapter 36: Measuring Rates of Reaction

Chapter 37: Factors Affecting Rates of Reaction

Chapter 38: Molar Volume of Gases

Branch: Physical Chemistry

Scope:
- Measuring reaction rates
- Rate graphs
- Factors affecting rates
- Collision theory
- Catalysts
- Experimental design
- Molar volume of gases
- Gas stoichiometry

### Topic X - Chemical Equilibrium

Chapter 39: Dynamic Equilibrium

Chapter 40: Equilibrium Constant

Chapter 41: Le Chatelier's Principle

Branches:
- Physical Chemistry
- Inorganic Chemistry

Scope:
- Reversible reactions
- Dynamic equilibrium
- Equilibrium constant Kc
- Kc calculations
- Effects of concentration and temperature
- Equilibrium shifts
- Industrial applications

### Topic XI - Chemistry of Carbon Compounds

Chapter 42: Advanced Homologous Series

Chapter 43: Isomerism

Chapter 44: Typical Reactions of Functional Groups

Chapter 45: Interconversions of Functional Groups

Chapter 46: Important Organic Substances

Branch: Organic Chemistry

Scope:
- Organic nomenclature
- Structural, cis-trans and optical isomerism
- Functional groups
- Reagents, conditions and observations
- Organic conversions
- Identification of compounds
- Aspirin, detergents, nylon and polyesters

### Topic XII - Patterns in the Chemical World

Chapter 47: Physical Properties of Period 2 Elements

Chapter 48: Acid-Base Properties of Period 3 Element Oxides

Chapter 49: Transition-Metal Properties

Branch: Inorganic Chemistry

Scope:
- Periodic trends
- Bonding and structure
- Melting points and conductivity
- Period 3 oxides
- Acid-base properties
- Transition-metal colours
- Variable oxidation states
- Catalytic properties

### Topic XIII - Industrial Chemistry

Chapters 50-51: Rate Equations

Chapter 52: Activation Energy

Chapter 53: Catalysis

Chapter 54: Industrial Processes

Chapter 55: Green Chemistry

Branch: Industrial Chemistry

Scope:
- Rate equations and reaction orders
- Rate constants
- Activation energy
- Catalysis
- Industrial processes
- Yield and atom economy
- Process optimisation
- Green chemistry

### Topic XIV - Materials Chemistry

Chapters 56-60: Individual titles not provided

Branch: Materials Chemistry

Scope:
- Cellulose and chitin
- Synthetic polymers
- Thermoplastics and thermosetting plastics
- Polymeric biomaterials
- Biodegradable plastics
- Alloys
- Liquid crystals
- Nanomaterials
- Green materials production

Do not invent titles for Chapters 56-60.

### Topic XV - Analytical Chemistry

Chapter 61: Identification Tests

Chapter 62: Separation Techniques

Chapter 63: Quantitative Analysis

Chapters 64-65: Instrumental Analysis

Branch: Analytical Chemistry

Scope:
- Identification tests
- Separation methods
- Chromatography
- Purity determination
- Volumetric analysis
- Quantitative calculations
- Error minimisation
- Colorimetry
- Infrared spectroscopy
- Mass spectrometry
- Applications of analytical chemistry

## Quality Checks

- Confirm the counted number of MCQs and structured questions matches the paper instructions.
- Check that every question number appears exactly once in the mapping.
- Use the user's syllabus wording for chapter names.
- Keep uncertainty local: mark only the affected question as "diagram-dependent" instead of weakening the whole analysis.
- Do not provide answer keys unless the user asks.
