# PRD: DeepDive (الغوص العميق)
## AI-Augmented Consultation Platform for Expert Advisory Work

**Version:** 3.0  
**Date:** February 16, 2026  
**Author:** Dr. Faisal Alotaibi  
**Context:** Enterprise consultation teams with high-volume advisory work

---

## 1. Executive Summary

DeepDive is an AI-augmented consultation tool designed for **domain experts** who need to:
1. Cover every corner of a topic (surface unknown unknowns)
2. Challenge their own thinking with diverse perspectives
3. Generate structured deliverables (MBB-style slides, formal reports)

**Core insight:** Consultants and experts are made over years of experience. They have deep domain knowledge. But they can't know everything — and they often struggle to structure their insights into polished deliverables.

**DeepDive is:**
- Expert + AI working together
- Human guides the discussion, AI challenges and fills gaps
- Output is a structured report, not a chat transcript

**DeepDive is NOT:**
- AI replacing consultants
- Pure automation
- Generic research tool

> "Not human alone. Not AI alone. Both working together."

---

## 2. The Problem

### What Consultants Have
- ✅ Deep domain expertise (years of experience)
- ✅ Contextual knowledge (client relationships, politics)
- ✅ Human judgment for nuanced recommendations

### What Consultants Lack
- ❌ Coverage of adjacent domains ("What about regulatory implications?")
- ❌ Time to research every angle
- ❌ Ability to self-challenge their blind spots
- ❌ Skills to structure insights into MBB-quality slides
- ❌ Consistent report formatting across projects

### Current Workflow Pain Points

| Step | Problem |
|------|---------|
| **Research** | Expert knows their domain but misses adjacent angles |
| **Structuring** | Hours spent formatting instead of thinking |
| **Quality** | Inconsistent deliverable quality across consultants |
| **Coverage** | Client asks "Did you consider X?" — often no |
| **Time** | Senior experts spend time on formatting, not expertise |

---

## 3. Vision

> "Every consultant produces comprehensive, well-structured deliverables — regardless of their formatting skills."

**How it works:**

```
┌─────────────────────────────────────────────────────────────┐
│                     CONSULTANT WORKFLOW                     │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. Expert enters the consultation topic/question           │
│                         ↓                                   │
│  2. DeepDive generates diverse AI perspectives              │
│     (regulatory, technical, financial, operational, etc.)   │
│                         ↓                                   │
│  3. AI perspectives discuss — expert observes               │
│     "What about data sovereignty?"                          │
│     "Have you considered the budget cycle?"                 │
│                         ↓                                   │
│  4. Expert interjects to guide/correct/focus                │
│     "Actually, the client already ruled out cloud..."       │
│                         ↓                                   │
│  5. Discussion surfaces unknown unknowns                    │
│     "Interesting point about workforce training..."         │
│                         ↓                                   │
│  6. Mind map captures all discovered angles                 │
│                         ↓                                   │
│  7. Generate structured report (MBB slides / formal doc)    │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 4. Target Users

### Primary: Consultation Teams & Advisory Firms
- Strategy consultants and domain experts
- Government advisory units
- In-house consulting departments
- Deliverables: Strategic recommendations, roadmaps, governance frameworks

### User Personas

| Persona | Profile | Pain Point | DeepDive Value |
|---------|---------|------------|----------------|
| **Senior Consultant** | 10+ years experience, deep expertise | Blind spots in adjacent domains | AI surfaces angles they'd miss |
| **Junior Consultant** | Strong research skills, limited experience | Can't structure MBB-quality output | Structured report generation |
| **Department Head** | Reviews all deliverables | Inconsistent quality across team | Standardized output format |
| **External Expert** | SME brought in for specific project | Knows domain, not house style | Template-driven deliverables |

---

## 5. Core Features

### 5.1 Dynamic Perspective Generation

**Input:** Consultation topic + context
**Output:** 3-5 AI perspectives relevant to THIS specific engagement

Unlike fixed personas (Steve Jobs, Elon Musk), DeepDive generates perspectives based on:
- The topic domain
- The client context (government, enterprise, startup)
- The deliverable type (strategy, implementation, assessment)

**Example:**
```
Topic: "AI adoption roadmap for Ministry of Health"

Generated Perspectives:
1. Healthcare IT Specialist — EHR integration, interoperability
2. AI Ethics Advisor — Patient privacy, algorithmic bias
3. Change Management Expert — Workforce adoption, training
4. Public Procurement Specialist — Budget cycles, vendor selection
5. Regulatory Compliance Officer — compliance requirements, data residency
```

### 5.2 Guided Discussion Mode

**Expert as Moderator:**
- Observe AI perspectives discussing
- Interject to correct/focus/guide
- Add context AI doesn't have ("The client already tried X")
- Request deeper exploration ("Tell me more about Y")

**Turn Management:**
1. Perspectives take turns (round-robin)
2. After 3 answer-only turns → system prompts new direction
3. Expert can interject anytime → overrides auto-flow
4. Discussion continues until expert is satisfied

### 5.3 Unknown Unknowns Discovery

The core value proposition:

| Traditional Approach | DeepDive Approach |
|---------------------|-------------------|
| Expert answers what they know | AI challenges with what expert might miss |
| Client asks → Consultant researches | Consultant discovers before client asks |
| Gaps found in review | Gaps surfaced during creation |

**Mechanisms:**
- Multiple perspectives = multiple angles of attack
- Moderator AI asks "thought-provoking questions"
- Retrieval brings in external information
- Mind map shows coverage (and gaps)

### 5.4 Live Mind Map

Visual knowledge organization during discussion:

```
AI Adoption Roadmap — Ministry of Health
├── Technical Infrastructure
│   ├── Current EHR systems
│   ├── Cloud readiness
│   └── Data integration requirements
├── Workforce & Change
│   ├── Training needs assessment
│   ├── Resistance factors
│   └── Champion identification
├── Governance & Compliance
│   ├── regulatory compliance
│   ├── Patient consent frameworks
│   └── Audit requirements
├── Financial
│   ├── CAPEX vs OPEX models
│   ├── Budget cycle timing
│   └── ROI projections
└── [GAP] Vendor Ecosystem
    └── (Not yet discussed — moderator will prompt)
```

### 5.5 Structured Report Generation

**The key differentiator:** Not just a transcript — a formatted deliverable.

**Output Options:**

| Format | Use Case |
|--------|----------|
| **MBB Slides** | Executive presentations, board briefings |
| **Formal Report** | Detailed recommendations, technical assessments |
| **Executive Summary** | 1-2 page decision document |
| **Action Plan** | Implementation roadmap with owners/timelines |

**Report Structure:**
- Mind map → Outline
- Discussion → Content (with citations)
- AI polish → Professional language
- Template → Consistent corporate branding

---

## 6. Technical Architecture

### 6.1 System Flow

```
┌─────────────┐     ┌─────────────────┐     ┌─────────────┐
│   Expert    │────▶│    DeepDive     │────▶│  Deliverable │
│   Input     │     │     Engine      │     │   Output     │
└─────────────┘     └────────┬────────┘     └─────────────┘
                             │
         ┌───────────────────┼───────────────────┐
         ▼                   ▼                   ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│   Perspective   │ │    Moderator    │ │    Retrieval    │
│    Agents       │ │     Agent       │ │     Engine      │
└─────────────────┘ └─────────────────┘ └─────────────────┘
                             │
                    ┌────────▼────────┐
                    │   Mind Map      │
                    │   + Gap Tracker │
                    └────────┬────────┘
                             │
                    ┌────────▼────────┐
                    │    Report       │
                    │   Generator     │
                    └─────────────────┘
```

### 6.2 MBB Slide Template

Each slide follows McKinsey-style structure:

```
┌─────────────────────────────────────────────────────────────┐
│ [GOVERNING THOUGHT — One sentence headline]                 │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  • Supporting point 1                                       │
│    - Detail                                                 │
│    - Evidence                                               │
│                                                             │
│  • Supporting point 2                                       │
│    - Detail                                                 │
│    - Evidence                                               │
│                                                             │
│  • Supporting point 3                                       │
│    - Detail                                                 │
│    - Evidence                                               │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│ Source: [Citations]                              Page X     │
└─────────────────────────────────────────────────────────────┘
```

---

## 7. Integration Points

### 7.1 organization Knowledge Base
- Connect to internal documentation
- Reference previous consultation reports
- Align with regulatory guidelines

### 7.2 Export Formats
- PowerPoint (.pptx) for MBB slides
- Word (.docx) for formal reports
- PDF for distribution
- Markdown for version control

### 7.3 Future: PPTXSmart Integration
- Generate slides directly into PowerPoint
- Apply corporate branding
- Use Slide Library templates

---

## 8. MVP Scope

### Phase 1: Core Loop (Weeks 1-4)
- [ ] Topic input → Perspective generation (3-4 agents)
- [ ] Round-robin discussion with expert interjection
- [ ] Basic moderator (intervene after stagnation)
- [ ] Simple mind map (read-only tree view)
- [ ] Chat-style UI (Arabic + English)
- [ ] Basic report export (Markdown)

### Phase 2: Report Quality (Weeks 5-8)
- [ ] MBB slide template
- [ ] Formal report template
- [ ] PowerPoint export
- [ ] Word export
- [ ] Citation management

### Phase 3: Enterprise (Weeks 9-12)
- [ ] internal knowledge base integration
- [ ] Project management (save/load consultations)
- [ ] Team collaboration
- [ ] Analytics (topics covered, gaps identified)

---

## 9. Success Metrics

### Efficiency
| Metric | Current | Target |
|--------|---------|--------|
| Time to first draft | 2-3 days | 2-3 hours |
| Revision cycles | 3-4 rounds | 1-2 rounds |
| Coverage gaps found in review | 30%+ | <10% |

### Quality
| Metric | Target |
|--------|--------|
| Expert satisfaction | 4.5/5 |
| Client feedback | "Comprehensive" rating 80%+ |
| Unknown unknowns surfaced per session | 3+ |

### Adoption
| Metric | 3-Month Target |
|--------|----------------|
| Active consultants using DeepDive | 8/10 team members |
| Projects using DeepDive | 50%+ of new projects |
| Reports generated | 50+ |

---

## 10. Competitive Positioning

| Tool | What It Does | Why DeepDive Is Different |
|------|--------------|---------------------------|
| ChatGPT | Q&A, single perspective | Multi-perspective, structured output |
| Perplexity | Research with citations | Not consultation-focused, no report gen |
| Co-STORM | Research curation | Academic, not enterprise deliverables |
| Notion AI | Document assistance | No multi-agent discourse |
| **DeepDive** | Expert + AI collaboration → MBB deliverables | Purpose-built for consultation work |

---

## 11. References

### Academic Foundation
- **Co-STORM:** Stanford OVAL Lab, EMNLP 2024
- **STORM:** Stanford, NAACL 2024

### Implementation Reference
- GitHub: https://github.com/stanford-oval/storm
- Python Package: `pip install knowledge-storm`

---

*Document ends.*
