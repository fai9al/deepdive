# Co-STORM: Complete Reference Documentation
> Source: Stanford OVAL Lab Research + Dr. Faisal's compilation
> EMNLP 2024

---

## Overview

Co-STORM (Collaborative STORM) is an advanced human-AI collaborative system developed by Stanford's OVAL Lab that transforms the automated research generation capabilities of STORM into an interactive, multi-agent discourse environment.

**Key Innovation:** Co-STORM converts the pre-writing research phase into a collaborative discourse where human users can observe, intervene, and steer conversations between AI agents to produce tailored, high-quality research outputs.

---

## What is STORM?

STORM (Synthesis of Topic Outlines through Retrieval and Multi-perspective Question Asking) is the foundation system that Co-STORM extends.

**STORM's Two-Stage Process:**
- **Pre-writing Stage:** Internet-based research, reference collection, and outline generation
- **Writing Stage:** Article generation based on outline and sources

Published in NAACL 2024, STORM achieved **25% better organization** and **10% broader coverage** compared to baseline methods according to Wikipedia editor evaluations.

---

## Core Concepts

### 1. Collaborative Discourse Model
Co-STORM implements a mixed-initiative system based on Eric Horvitz's principles (1999), allowing both AI agents and human users to initiate actions and contribute to the conversation flow.

### 2. Multi-Agent Roundtable

| Role | Function |
|------|----------|
| **LLM Experts** | Provide grounded answers from external sources or generate insightful follow-up questions based on conversation history |
| **Moderators** | Facilitate discussions by asking thought-provoking questions inspired by unexplored information |
| **Human Users** | Observe for passive learning or actively participate to steer conversations toward specific needs |

### 3. Dynamic Mind Map
A concept-oriented hierarchical visualization that:
- Structures retrieved information in real-time
- Creates a shared conceptual space between user and system
- Reduces cognitive load during long discussions
- Enables exploration of knowledge relationships

---

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                 Co-STORM System Architecture                │
├─────────────────────────────────────────────────────────────┤
│ ┌──────────────┐ ┌──────────────┐ ┌──────────────────┐      │
│ │    Human     │ │  Moderator   │ │  LLM Expert(s)   │      │
│ │    User      │◄─┤    Agent     │◄─┤   (Multi-turn)   │      │
│ └──────┬───────┘ └──────┬───────┘ └──────────────────┘      │
│        │                │                                    │
│        └────────┬───────┘                                   │
│                 ▼                                           │
│        ┌─────────────────┐                                  │
│        │    Discourse    │                                  │
│        │    Manager      │                                  │
│        └────────┬────────┘                                  │
│                 ▼                                           │
│        ┌─────────────────┐                                  │
│        │  Dynamic Mind   │                                  │
│        │   Map Engine    │                                  │
│        └────────┬────────┘                                  │
│                 ▼                                           │
│        ┌─────────────────┐                                  │
│        │     Report      │                                  │
│        │    Generator    │                                  │
│        └─────────────────┘                                  │
└─────────────────────────────────────────────────────────────┘
```

### Workflow
1. **Warm Start:** Initialize the collaborative environment
2. **Discourse Loop:** Multi-turn conversations between agents with optional human intervention
3. **Knowledge Accumulation:** Dynamic mind map updates with each turn
4. **Report Generation:** Final structured output based on curated discussion

---

## Key Features

### 1. Collaborative Human-AI Interaction
- **Passive Mode:** Observe AI-to-AI discourse for comprehensive topic understanding
- **Active Mode:** Inject inputs, steer conversations, request deeper exploration on specific aspects

### 2. Dynamic Multi-Agent Discussion
- Multiple AI agents simulate diverse expert perspectives
- Conversations evolve based on previous answers (multi-turn coherence)
- Moderator agent identifies knowledge gaps and probes deeper

### 3. Concept-Oriented Mind Map
- Visual knowledge hierarchy updated in real-time
- Concept relationships mapped dynamically
- Facilitates non-linear exploration of topics

### 4. Grounded Information Retrieval
- All claims supported by external sources
- Retrieval-augmented generation (RAG) architecture
- Source attribution for verification

### 5. Flexible Report Generation
- On-demand report creation from discussion history
- Structured, citation-rich output
- Exportable formats (PDF, Markdown)

---

## Installation

### Via pip
```bash
pip install knowledge-storm
```

### From Source
```bash
git clone https://github.com/stanford-oval/storm.git
cd storm
pip install -e .
```

### Dependencies
- `openai` or other LLM client libraries
- `qdrant-client` (for vector storage)
- `langchain` (optional, for extended implementations)
- Web search APIs (Bing, Google, Serper, etc.)

---

## Usage Guide

### Basic Setup
```python
from knowledge_storm import CoStormRunner

# Initialize Co-STORM runner
costorm_runner = CoStormRunner(
    topic="Your Research Topic",
    llm_config={
        "model": "gpt-4",
        "api_key": "your-api-key"
    },
    retriever_config={
        "search_api": "bing",
        "api_key": "your-search-key"
    }
)
```

### Running a Collaborative Session
```python
# Warm start the system
costorm_runner.warm_start()

# Option 1: Observe AI-only discussion
for i in range(5):
    conv_turn = costorm_runner.step()
    print(f"Turn {i+1}: {conv_turn}")

# Option 2: Actively participate
user_input = "Can you explore the economic implications in more detail?"
conv_turn = costorm_runner.step(user_utterance=user_input)

# Generate final report
article = costorm_runner.generate_report()
print(article)
```

### Accessing the Mind Map
```python
# Get current knowledge structure
mind_map = costorm_runner.get_mind_map()

# Explore specific concepts
related_concepts = mind_map.get_related("specific concept")
```

### Web Interface
Stanford provides a live demo at: https://storm.genie.stanford.edu

---

## System Components

### 1. Co-STORM Agents
**File:** `knowledge_storm/collaborative_storm/modules/co_storm_agents.py`

Customizable LLM agents with specific personas:
- **Expert Agents:** Domain specialists with retrieval capabilities
- **Moderator Agent:** Facilitates discourse, identifies gaps

### 2. Discourse Manager
**File:** `knowledge_storm/collaborative_storm/engine.py`

Manages turn-taking policies:
- Determines which agent speaks next
- Handles human intervention points
- Maintains conversation coherence

### 3. Dynamic Mind Map
**Implementation:** Concept-oriented hierarchy engine
- **Node Types:** Topics, subtopics, entities, claims
- **Relationships:** Hierarchical, causal, associative
- **Updates:** Real-time as new information emerges

### 4. Report Generator
Transforms discourse history into structured articles:
- Outline extraction from mind map
- Section generation with citations
- Polish and formatting

---

## Evaluation & Performance

### Human Evaluation Results (EMNLP 2024)

Compared to baseline RAG chatbots and STORM+QA:

| Metric | RAG Chatbot | STORM+QA | Co-STORM |
|--------|-------------|----------|----------|
| Relevance | 3.57 | 3.61 | **3.78** |
| Breadth | 3.50 | 3.61 | **3.79** |
| Depth | 3.26 | 3.43 | **3.77** (+) |
| Novelty | 2.44 | 2.50 | **3.05** (+) |
| Info Diversity | 0.595 | 0.592 | **0.602** |

(+) indicates statistically significant improvement

### Ablation Studies

| Configuration | Relevance | Breadth | Depth | Novelty |
|--------------|-----------|---------|-------|---------|
| Full Co-STORM | 3.78 | 3.79 | 3.77 | 3.05 |
| w/o Multi-Expert | 3.73 | 3.75 | 3.77 | 2.93 |
| w/o Moderator | 3.56 | 3.69 | 3.41 | 2.89 |

**Key Finding:** The moderator role is **critical** for depth and novelty; multi-expert setup improves breadth.

### User Study Insights
- 20 participants in controlled study
- Users valued ability to steer conversations toward "unknown unknowns"
- Dynamic mind map reduced cognitive load in complex topics
- **Collaboration pattern:** Users typically observe 3-4 turns before intervening

---

## Research Background

### Theoretical Foundation
Co-STORM is based on research into:
- **Human writing processes** (Rohman, 1965): Pre-writing as discovery
- **Research methodology** (Booth et al., 2003): Question-driven investigation
- **Mixed-initiative interfaces** (Horvitz, 1999): Balancing automation and control
- **Collaborative learning:** Educational discourse models

### From STORM to Co-STORM

**Problem Identified:** STORM generates comprehensive articles, but users often need to:
- Explore specific aspects more deeply
- Incorporate personal knowledge
- Verify and challenge AI-generated claims
- Learn through participation rather than consumption

**Solution:** Convert the pre-writing stage from automated simulation to collaborative discourse, allowing users to engage with AI agents as co-researchers.

---

## Limitations & Future Work

### Current Limitations
1. **Multimodal Support:** Text-only; no images, charts, or data visualization
2. **Quality Ceiling:** Not yet at experienced human researcher level
3. **Reference Nuances:** Citation formatting and source verification need refinement
4. **Latency:** Real-time multi-agent discussion requires significant compute
5. **Scope:** Optimized for Wikipedia-style articles; other formats need adaptation

### Future Directions
- Enhanced Moderator: More sophisticated gap detection algorithms
- Personalization: User preference learning for discourse style
- Integration: Connect with external knowledge bases (Notion, Zotero)
- Multimodal: Support for charts, images, and data tables
- Offline Mode: Local LLM support for sensitive research

---

## References

1. **STORM Paper:** Shao, Y., Jiang, Y., Kanell, T. A., Xu, P., Khattab, O., & Lam, M. S. (2024). "Assisting in writing Wikipedia-like articles from scratch with large language models." NAACL 2024.

2. **Co-STORM Paper:** Jiang, Y., Shao, Y., Ma, D., Semnani, S. J., & Lam, M. S. (2024). "Into the Unknown Unknowns: Engaged Human Learning through Participation in Language Model Agent Conversations." EMNLP 2024.

3. **GitHub Repository:** https://github.com/stanford-oval/storm

4. **Live Demo:** https://storm.genie.stanford.edu

5. **Stanford OVAL Lab:** https://oval.cs.stanford.edu/

---

## Citation

```bibtex
@inproceedings{jiang2024unknown,
  title={Into the Unknown Unknowns: Engaged Human Learning through Participation in Language Model Agent Conversations},
  author={Jiang, Yucheng and Shao, Yijia and Ma, Dekun and Semnani, Sina J and Lam, Monica S},
  booktitle={EMNLP 2024},
  year={2024}
}

@inproceedings{shao2024storm,
  title={Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models},
  author={Shao, Yijia and Jiang, Yucheng and Kanell, Theodore A and Xu, Peter and Khattab, Omar and Lam, Monica S},
  booktitle={NAACL 2024},
  year={2024}
}
```

---

## License
MIT License - Stanford OVAL Lab

---

> **Note:** Co-STORM is a research preview. Generated content may contain errors; always verify important information. The system collects interaction data for research purposes under Creative Commons Attribution (CC-BY) license.
