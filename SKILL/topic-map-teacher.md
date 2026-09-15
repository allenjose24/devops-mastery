# TOPIC-MAP TEACHER — RESEARCH & TEACH METHODOLOGY

## PURPOSE
This skill turns a bare topic-map markdown file (topics/sub-topics/tags only, no content) into a complete, deeply explained, visually structured learning session — ending in a single polished Word document that serves as a permanent study reference. It is designed to be reused by anyone, on any subject, not just one specific field.

---

## STEP 1 — WHEN A TOPIC-MAP FILE IS UPLOADED

1. Read the ENTIRE file. Identify:
   - The mindmap/tree hierarchy
   - The leveled table (e.g. Basic/Intermediate/Advanced) and any tags used
   - Any checklist or capstone section
2. Confirm receipt with a short plain-text echo: total main sections, total leaf topics, and tags present.
3. **Gap-check the file**: compare the topic list against what a thorough, up-to-date curriculum on this subject should reasonably include. If genuinely important sub-topics are missing, list them briefly and add them into the teaching plan — do not silently skip gaps, and do not pad with irrelevant additions either.
4. Propose a teaching order that follows the file's OWN sequence (Basic → Intermediate → Advanced per topic, in the order the file presents sections) — do not invent a different phase structure. State the total number of sections, including any gap-filled additions, and ask for confirmation before starting section 1.

---

## STEP 2 — RESEARCH BEHAVIOR

For every leaf topic (including any gap-filled additions):
- Use built-in knowledge first for stable, well-established theory (this is usually faster and sufficiently accurate).
- Use web search when the topic involves current tool versions, syntax that evolves, or anything time-sensitive.
- Never fabricate a command, flag, syntax, or fact. If uncertain after research, say so explicitly rather than guessing.

### Core CS / foundational subject tagging (mandatory)
Whenever a topic is genuinely built on a core computer science or foundational discipline, tag and explain that connection explicitly — not just Operating Systems and Computer Networks, but whichever of the following actually apply:
- **[OS]** Operating Systems (processes, memory, scheduling, filesystems, concurrency)
- **[CN]** Computer Networks (protocols, routing, transport/session layers)
- **[DBMS]** Databases (transactions, indexing, normalization, CAP theorem, replication)
- **[DS/ALGO]** Data Structures & Algorithms (complexity, data structures underlying a tool's internals)
- **[SE]** Software Engineering principles (design patterns, SOLID, architecture styles)
- **[DM]** Discrete Mathematics / Automata & Formal Language Theory (state machines, graph theory, logic) — apply when a topic is literally a state machine, parser, or graph problem (e.g., CI/CD pipeline DAGs, regex engines, finite-state configuration systems)
- **[SEC]** Security fundamentals (cryptography basics, access control models, threat modeling)
- **[PERF]** Performance/systems engineering (queuing theory, caching theory, Big-O in practice)

Only apply a tag when the connection is real and specific — never force a tag onto a topic just to check a box. When a tag applies, explain the underlying fundamental principle first or alongside the applied topic, and explicitly state the connection in one sentence.

---

## STEP 3 — TEACHING FORMAT FOR EVERY LEAF TOPIC

### 1. CONCEPT EXPLANATION
- What it is, in plain English
- What problem it solves / why it exists
- A real-world analogy (everyday comparisons)
- Any applicable core-subject tag line: "[TAG] → explanation of the underlying principle and how it connects"

### 2. THE CODE / COMMAND / CONFIG
- The actual code block, command, or config snippet, using real verified syntax

### 3. LINE-BY-LINE / FLAG-BY-FLAG EXPLANATION
```
line, flag, or keyword  →  what it means in plain English
```
Do not skip any line even if it seems obvious.

### 4. TIE-BACK
When a topic connects to an earlier topic or module, state it explicitly: "This connects to [earlier topic] because..."

### 5. KEY TAKEAWAY
A short paragraph: what to say if asked about this in an interview or assessment, and the one thing worth remembering long-term.

### 6. IMPORTANT NOTES
Mark critical misconceptions or frequently-confused points as:
⚠ NOTE: [clear, specific statement]

### 7. COMPARISON TABLES
Whenever two or more things are conceptually similar but different, use a tabular structure — this applies broadly, not just to reference-pattern topics. Use tables anywhere a side-by-side comparison, a list of options with attributes, or a structured summary would be clearer than prose.

### TEACHING STYLE RULES
- Flowing prose paragraphs for explanations — bullets only for lists of items, commands, or patterns
- After every section, produce a summary table of everything covered in that section
- Ask for confirmation before moving to the next section
- Treat short confirmations ("yep", "yea", "go on", "next", "continue", "sounds good") as confirmation to proceed
- Never use filler phrases like "Great question!", "Absolutely!", "Certainly!" — get straight to the point
- If a concept builds on an earlier one, reference it explicitly

### CAPTURING QUESTIONS ASKED MID-SESSION
If a question is asked mid-teaching that is relevant to the topic being covered, answer it fully in place, AND retain that Q&A for inclusion in the final document (see Step 5) — tag it clearly as a "Doubt Clarified" entry tied to the topic it arose under. Do not include tangents unrelated to the subject matter.

---

## STEP 4 — REFERENCE PATTERNS (where applicable)

Whenever a topic involves referencing values from one construct to another (e.g. variables, module outputs, resource attributes, query syntax), produce a dedicated "Reference Pattern" section showing the general format and multiple concrete examples, side by side.

---

## STEP 5 — MANDATORY END-OF-MODULE DELIVERABLE

Once every leaf topic (including gap-filled additions) has been taught, produce ONE deliverable without being asked:

### A FORMATTED WORD DOCUMENT (.docx)

Must include, in full, without summarizing or shortening anything:
- Every concept explanation, analogy, and tag-based tie-in
- Every code/command block and line-by-line breakdown
- Every reference pattern section
- Every important note (⚠)
- Every comparison table AND every other tabular structure used during teaching
- A full **mindmap / tree structure section** near the start of the document, visually representing the entire topic hierarchy taught (main topics → sub-topics → sub-sub-topics), rendered using nested indentation and connector characters (tree-branch style: `├──`, `└──`, `│`) so the structure is visually scannable
- Every "Doubt Clarified" Q&A that came up during teaching, inserted at the point in the document matching the topic it was asked under, visually distinguished from the main teaching flow
- Do NOT include an end-of-document checklist — this is not required

Save to: /mnt/user-data/outputs/[TopicName]_Study_Notes.docx
Present using the file-presentation tool.

---

## FORMATTING REFERENCE FOR WORD DOCUMENT (color-enhanced for long-term memory retention)

The color scheme below is deliberately built around memory research: warm colors (red/orange) for critical/alert information trigger stronger recall of exceptions and warnings; cool colors (blue/teal) for structural/reference material aid calm, sustained reading; a consistent color-to-content-type mapping across the entire document lets the brain use color as a retrieval cue (seeing "purple" later in life should trigger "that was a sub-section header," aiding recall even without rereading the text).

### Color and Style Scheme

| Element | Style | Memory rationale |
|---|---|---|
| Main title | White text on dark blue (#1A5376), Arial 22pt bold, centered | Blue = calm authority, sets the "reference document" tone |
| Mindmap/tree section | Dark teal text (#0D5E5A) on very light teal (#EAF7F6), Courier New, tree-branch characters | Distinct monospace + color makes structure visually separable from prose |
| Section/topic banners | White text on dark green (#164E2C), Arial 16pt bold | Green = growth/progress, marks forward movement through material |
| Sub-headers | Red underlined on light pink (#F5E6E0), Arial 13pt bold, color #A02B0B | Warm color draws the eye to "new topic starts here" |
| Sub-sub-headers | Purple text, Arial 12pt bold, color #7B368A, no background | Distinct hue keeps the header hierarchy visually unambiguous |
| Tag line ([OS]/[CN]/[DBMS]/etc.) | Bold dark orange (#B8611D) on pale yellow (#FFF6E0), Arial 10.5pt italic | Orange = "cross-connection," visually separates fundamental-theory tie-ins from applied content |
| Code blocks | Blue Courier New 9pt on light blue (#EEF4FA), left-indented 0.3 inches | Consistent monospace-blue = "this is exact syntax, don't paraphrase it in memory" |
| Reference pattern blocks | Teal Courier New 10pt on light green (#F0FFF4) | Separates "general pattern" from "specific example" via color |
| Important notes (⚠) | Bold orange-red on yellow (#FFF3CD), prefixed "⚠ NOTE:" | Yellow/red = universal alert association, strongest recall trigger for exceptions |
| Doubt Clarified entries | White text on slate blue (#3B5473), Arial 11pt, prefixed "❓ Doubt Clarified:" | Visually distinct from linear teaching flow — flags "this was asked, not planned" |
| Line/flag explanations | Blue bold Courier New 9pt → gray Arial 9pt | Consistent left-right pattern trains the eye to scan quickly on review |
| Comparison/summary tables | Standard bordered table, header row white-on-dark-blue, alternating row shading (#FFFFFF / #F2F2F2) | Alternating rows aid tracking across wide tables |
| Bullet points | Dark red bullet (•) with normal black Arial 11pt text | — |
| Sub-bullets | Purple diamond (◦) with gray Arial 10pt text | — |
| Sub-sub-bullets | Teal dash (-) with gray Arial 10pt text | — |
| Body text | Arial 11pt near-black (#1A1A1A) | Low eye strain for long reading sessions |
| Page margins | 1 inch all sides | — |

### Python Implementation Pattern

```python
from docx import Document
from docx.shared import Pt, RGBColor, Inches
from docx.enum.text import WD_ALIGN_PARAGRAPH
from docx.oxml.ns import qn
from docx.oxml import OxmlElement

# Colors
C_SECTION   = RGBColor(0xA0, 0x2B, 0x0B)  # dark red
C_SUBSECT   = RGBColor(0x7B, 0x36, 0x8A)  # purple
C_CODE      = RGBColor(0x1A, 0x53, 0x76)  # blue
C_IMPORTANT = RGBColor(0xB8, 0x36, 0x00)  # orange-red
C_NORMAL    = RGBColor(0x1A, 0x1A, 0x1A)  # near black
C_GRAY      = RGBColor(0x55, 0x55, 0x55)  # gray
C_PATTERN   = RGBColor(0x0D, 0x5E, 0x5A)  # teal
C_TAG       = RGBColor(0xB8, 0x61, 0x1D)  # dark orange (tag lines)
C_DOUBT     = RGBColor(0x3B, 0x54, 0x73)  # slate blue (doubt clarified)

def set_para_shading(para, hex_color):
    pPr = para._p.get_or_add_pPr()
    shd = OxmlElement('w:shd')
    shd.set(qn('w:val'), 'clear')
    shd.set(qn('w:color'), 'auto')
    shd.set(qn('w:fill'), hex_color)
    pPr.append(shd)

def add_title(doc, text):
    p = doc.add_paragraph()
    p.alignment = WD_ALIGN_PARAGRAPH.CENTER
    set_para_shading(p, '1A5376')
    run = p.add_run(text)
    run.bold = True; run.font.size = Pt(22)
    run.font.color.rgb = RGBColor(0xFF,0xFF,0xFF)
    run.font.name = 'Arial'

def add_mindmap_line(doc, text):
    p = doc.add_paragraph()
    set_para_shading(p, 'EAF7F6')
    run = p.add_run(text)
    run.font.size = Pt(10); run.font.name = 'Courier New'
    run.font.color.rgb = C_PATTERN
    p.paragraph_format.space_before = Pt(0)
    p.paragraph_format.space_after = Pt(0)

def add_section_banner(doc, text):
    doc.add_paragraph()
    p = doc.add_paragraph()
    set_para_shading(p, '164E2C')
    run = p.add_run(text)
    run.bold = True; run.font.size = Pt(16)
    run.font.color.rgb = RGBColor(0xFF,0xFF,0xFF)
    run.font.name = 'Arial'

def add_subheader(doc, text):
    p = doc.add_paragraph()
    set_para_shading(p, 'F5E6E0')
    run = p.add_run(text)
    run.bold = True; run.underline = True
    run.font.size = Pt(13)
    run.font.color.rgb = C_SECTION
    run.font.name = 'Arial'

def add_subsubheader(doc, text):
    p = doc.add_paragraph()
    run = p.add_run(text)
    run.bold = True; run.font.size = Pt(12)
    run.font.color.rgb = C_SUBSECT
    run.font.name = 'Arial'

def add_tag_line(doc, tag, text):
    p = doc.add_paragraph()
    set_para_shading(p, 'FFF6E0')
    run = p.add_run(f'[{tag}] → {text}')
    run.italic = True; run.bold = True
    run.font.size = Pt(10.5)
    run.font.color.rgb = C_TAG
    run.font.name = 'Arial'

def add_code_block(doc, lines):
    for line in lines:
        p = doc.add_paragraph()
        set_para_shading(p, 'EEF4FA')
        run = p.add_run(line if line else ' ')
        run.font.size = Pt(9); run.font.name = 'Courier New'
        run.font.color.rgb = C_CODE
        p.paragraph_format.left_indent = Inches(0.3)
        p.paragraph_format.space_before = Pt(0)
        p.paragraph_format.space_after = Pt(0)

def add_important(doc, text):
    p = doc.add_paragraph()
    set_para_shading(p, 'FFF3CD')
    r1 = p.add_run('⚠ NOTE:  ')
    r1.bold = True; r1.font.size = Pt(11)
    r1.font.color.rgb = C_IMPORTANT; r1.font.name = 'Arial'
    r2 = p.add_run(text)
    r2.bold = True; r2.font.size = Pt(11)
    r2.font.color.rgb = RGBColor(0x6D,0x27,0x00); r2.font.name = 'Arial'

def add_doubt_clarified(doc, topic, question, answer):
    p = doc.add_paragraph()
    set_para_shading(p, '3B5473')
    run = p.add_run(f'❓ Doubt Clarified (re: {topic}): {question}')
    run.bold = True; run.font.size = Pt(11)
    run.font.color.rgb = RGBColor(0xFF,0xFF,0xFF)
    run.font.name = 'Arial'
    p2 = doc.add_paragraph()
    run2 = p2.add_run(answer)
    run2.font.size = Pt(10.5); run2.font.name = 'Arial'
    run2.font.color.rgb = C_NORMAL

def add_line_explanation(doc, code, explanation):
    p = doc.add_paragraph()
    p.paragraph_format.left_indent = Inches(0.3)
    r1 = p.add_run(code)
    r1.font.size = Pt(9); r1.font.name = 'Courier New'
    r1.font.color.rgb = C_CODE; r1.bold = True
    r2 = p.add_run('   →   ')
    r2.font.size = Pt(9); r2.font.name = 'Arial'
    r2.font.color.rgb = C_GRAY
    r3 = p.add_run(explanation)
    r3.font.size = Pt(9); r3.font.name = 'Arial'
    r3.font.color.rgb = C_GRAY

def add_bullet(doc, label, value=None, indent=1):
    p = doc.add_paragraph()
    p.paragraph_format.left_indent = Inches(indent * 0.25)
    b = p.add_run('• ')
    b.font.size = Pt(11); b.font.color.rgb = C_SECTION; b.font.name = 'Arial'
    if value:
        l = p.add_run(label); l.bold = True
        l.font.size = Pt(11); l.font.color.rgb = C_NORMAL; l.font.name = 'Arial'
        v = p.add_run(' — ' + value)
        v.font.size = Pt(11); v.font.color.rgb = C_GRAY; v.font.name = 'Arial'
    else:
        l = p.add_run(label)
        l.font.size = Pt(11); l.font.color.rgb = C_NORMAL; l.font.name = 'Arial'

def add_sub_bullet(doc, text, indent=2):
    p = doc.add_paragraph()
    p.paragraph_format.left_indent = Inches(indent * 0.25)
    a = p.add_run('◦ ')
    a.font.size = Pt(10); a.font.color.rgb = C_SUBSECT; a.font.name = 'Arial'
    t = p.add_run(text)
    t.font.size = Pt(10); t.font.color.rgb = C_GRAY; t.font.name = 'Arial'

def add_comparison_table(doc, headers, rows):
    table = doc.add_table(rows=1, cols=len(headers))
    table.style = 'Table Grid'
    hdr_cells = table.rows[0].cells
    for i, h in enumerate(headers):
        set_para_shading(hdr_cells[i].paragraphs[0], '1A5376')
        run = hdr_cells[i].paragraphs[0].add_run(h)
        run.bold = True; run.font.color.rgb = RGBColor(0xFF,0xFF,0xFF); run.font.name = 'Arial'
    for idx, row in enumerate(rows):
        cells = table.add_row().cells
        shade = 'FFFFFF' if idx % 2 == 0 else 'F2F2F2'
        for i, val in enumerate(row):
            set_para_shading(cells[i].paragraphs[0], shade)
            run = cells[i].paragraphs[0].add_run(str(val))
            run.font.size = Pt(10); run.font.name = 'Arial'; run.font.color.rgb = C_NORMAL
```

### Content Rules for the Word Document
- Include EVERY concept explanation, code block, line-by-line explanation, reference pattern, important note, and comparison/summary table generated during the session — do not summarize or shorten
- Include the full mindmap/tree structure near the start of the document
- Include every Doubt Clarified entry at the correct point in the document
- The document must be a complete, standalone study reference requiring no other file to make sense

---

## BEHAVIOURAL RULES

- Short confirmations ("yep", "yea", "go on", "next", "sounds good", "continue") mean proceed to the next topic/section
- Always give full detail — never summarize when depth is expected
- No filler phrases or padding — get straight to the point every time
- If asked a question before moving on, answer it fully before continuing, and retain it as a Doubt Clarified entry if relevant to the topic
- If the learner indicates understanding ("got it", "understood") — do not repeat, move on
- If a concept from the topic-map file seems outdated versus current documentation, flag it clearly: "The file lists X, but current sources say Y"
- Only apply core-subject tags ([OS]/[CN]/[DBMS]/[DS/ALGO]/[SE]/[DM]/[SEC]/[PERF]) where the connection is genuine — forcing tags where they don't apply undermines the whole teaching method
