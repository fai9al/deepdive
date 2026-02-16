# PRD: Advisory Roundtable (مجلس المستشارين)
## AI-Powered Collaborative Knowledge Curation Platform

**Version:** 2.0  
**Date:** February 16, 2026  
**Author:** Dr. Faisal Alotaibi  
**Inspiration:** Stanford Co-STORM (EMNLP 2024)

---

## 1. Executive Summary

An AI-powered platform that generates a panel of Subject Matter Experts (SMEs) based on any topic, facilitates autonomous multi-turn discussion between them, and allows users to observe passively or participate actively to steer the discourse.

**Core innovation:** Solving the "unknown unknowns" problem — helping users discover information they didn't know they were missing, through participation in expert conversations.

> *"Tell me and I forget. Teach me and I remember. Involve me and I learn."* — Benjamin Franklin

Unlike static persona-based advisors (afyaa.net) or single-turn QA systems, this platform:
- Dynamically assembles relevant experts per topic
- Experts discuss WITH each other (not just respond to user)
- Maintains a **live mind map** organizing discovered knowledge
- Generates a **cited report** as final deliverable

---

## 2. Problem Statement

**Current solutions (e.g., afyaa.net):**
- Fixed set of personas (Steve Jobs, Elon Musk, etc.)
- Each advisor responds independently — no interaction
- Limited to business/startup advice
- User asks, AI answers — linear, not dynamic

**What's missing:**
- Topic-adaptive expertise (not everyone needs Steve Jobs)
- Cross-pollination of ideas through discussion
- Ability to watch experts debate, agree, challenge each other
- Real-time moderation to redirect discourse

---

## 3. Vision

> "A virtual boardroom where the right experts are summoned for YOUR question, debate it among themselves, and you hold the gavel."

**Core differentiators:**
1. **Dynamic SME generation** — experts are synthesized based on topic, not pre-built
2. **Autonomous discussion** — SMEs respond to each other, not just the user
3. **User as moderator** — inject prompts to steer, challenge, or refocus
4. **Multi-domain** — works for business, tech, policy, health, anything

---

## 4. User Personas

| Persona | Description | Use Case |
|---------|-------------|----------|
| **Startup Founder** | Building a product, needs strategic input | "Should I pivot to B2B?" |
| **Executive** | Making high-stakes decisions | "How do we approach this acquisition?" |
| **Policy Maker** | Designing regulations/frameworks | "What are the risks of this AI policy?" |
| **Researcher** | Exploring complex topics | "Debate the merits of transformer vs. state-space models" |
| **Student/Learner** | Understanding multi-perspective issues | "Explain climate solutions from different angles" |

---

## 5. Core Features

### 5.1 Topic Input & SME Generation

**User action:** Enter a topic or question  
**System response:** Generate 3-5 relevant SMEs with:
- Name (can be real archetypes or synthetic personas)
- Expertise area
- Perspective/school of thought
- Brief bio

**Example:**
```
Topic: "Should Saudi Arabia invest heavily in nuclear energy?"

Generated Panel:
1. Dr. Khalid Al-Falih (Energy Policy) — pragmatic, pro-diversification
2. Prof. Amory Lovins (Renewable Energy) — skeptic, soft-path advocate  
3. Dr. Mohamed ElBaradei (Nuclear Governance) — safety/regulation lens
4. Eng. Sarah Al-Suhaimi (Finance/Investment) — ROI and capital allocation
5. Dr. Abdullah Al-Shehri (Environmental Science) — ecological impact focus
```

### 5.2 Autonomous Discussion Mode

Once panel is generated:
1. System initiates discussion with opening statements
2. SMEs respond to each other:
   - Agree and build on points
   - Respectfully challenge/counter
   - Ask clarifying questions to each other
   - Reference their expertise area
3. Discussion continues for N rounds (configurable, default: 3)

**UI shows:**
- Chat-style thread with expert avatars
- Clear attribution of who's speaking
- Visual indicators of agreement/disagreement
- "Discussion in progress..." animation between turns

### 5.3 User Moderation Controls

At any point, user can:

| Action | Effect |
|--------|--------|
| **Inject prompt** | SMEs pause, receive user input, resume discussion incorporating it |
| **Ask specific expert** | Direct question to one SME, others may respond |
| **Challenge** | Force SMEs to defend/reconsider a position |
| **Redirect** | "Let's focus on X instead" — shifts discussion topic |
| **Request consensus** | "Can you summarize where you agree/disagree?" |
| **Add expert** | Bring in additional SME mid-discussion |
| **Remove expert** | Dismiss an SME from the panel |

### 5.4 Discussion Output

After discussion concludes:
- **Summary:** Key points from each expert
- **Consensus view:** Where experts agreed
- **Contested points:** Unresolved debates
- **Recommended actions:** Synthesized next steps
- **Export:** PDF/Markdown report, shareable link

### 5.5 Session Management

- Save discussions to revisit later
- Fork discussions to explore alternate directions
- Share public link (view-only or collaborative)
- Continue previous sessions with new prompts

---

## 6. Technical Architecture (Co-STORM Inspired)

### 6.1 System Participants

```
┌─────────────────────────────────────────────────────────────────┐
│                     DISCOURSE MANAGER                           │
│              (Turn Policy + Initiative Control)                  │
└─────────────────────────┬───────────────────────────────────────┘
                          │
        ┌─────────────────┼─────────────────┐
        ▼                 ▼                 ▼
┌───────────────┐ ┌───────────────┐ ┌───────────────┐
│  LLM EXPERT   │ │  LLM EXPERT   │ │  LLM EXPERT   │
│   AGENTS      │ │   AGENTS      │ │   AGENTS      │
│ (N perspectives)│ │              │ │               │
└───────────────┘ └───────────────┘ └───────────────┘
        │                 │                 │
        └─────────────────┼─────────────────┘
                          ▼
              ┌───────────────────┐
              │  MODERATOR AGENT  │ ◀── Intervenes when stuck
              │  (Non-expert who  │
              │   asks good Qs)   │
              └───────────────────┘
                          │
                          ▼
              ┌───────────────────┐
              │    HUMAN USER     │ ◀── Can interject anytime
              │  (Observer OR     │
              │   Participant)    │
              └───────────────────┘
                          │
                          ▼
              ┌───────────────────┐
              │   DYNAMIC MIND    │ ◀── Live knowledge organization
              │       MAP         │
              │  (Tree structure) │
              └───────────────────┘
                          │
                          ▼
              ┌───────────────────┐
              │  REPORT GENERATOR │ ◀── Final cited deliverable
              └───────────────────┘
```

### 6.2 Turn Management Rules

```
1. WARM-UP: N experts each take one opening turn
2. ROUND-ROBIN: Experts take turns sequentially
3. MODERATOR INTERVENTION: After L consecutive answer-only turns 
   (no new questions), moderator injects new direction
4. USER OVERRIDE: User can inject at ANY time, overriding sequence
5. RETURN TO AUTO: After user input, system retrieves info, 
   potentially updates expert list, resumes auto-steering
```

**Parameters:**
- `N` = Number of experts (default: 3-5)
- `L` = Stagnation threshold (default: 3 consecutive answer-only turns)

### 6.3 Mixed-Initiative Control

| Mode | User Behavior | System Behavior |
|------|---------------|-----------------|
| **User Initiative** | Actively engages | Responds to user's question/argument |
| **Agent Initiative** | Observes passively | Auto-generates next turn |
| **Balanced** | Occasional interjection | Continues discourse, incorporates input |

The user controls the balance — they can passively learn OR actively direct.

### 6.4 Expert Pipeline (Per Turn)

```python
def expert_turn(expert, discourse_history, mind_map):
    # Step 1: Intent Selection
    intent = select_intent(expert, discourse_history)
    # Options: "question-asking" | "question-answering"
    
    if intent == "question-answering":
        # Step 2a: Retrieval
        query = generate_search_query(discourse_history)
        sources = web_search(query)
        response = generate_cited_response(expert, sources, discourse_history)
    else:
        # Step 2b: Question Generation
        response = generate_question(expert, discourse_history)
    
    # Step 3: Polishing
    polished = polish_utterance(response, style="conversational")
    
    # Step 4: Update Mind Map
    mind_map.insert(polished, sources)
    
    return polished
```

### 6.5 Moderator Pipeline

```python
def moderator_turn(discourse_history, unused_info, mind_map):
    # Step 1: Rerank unused information
    ranked_info = rerank_by_relevance(unused_info, discourse_history)
    
    # Step 2: Generate thought-provoking question
    question = generate_question(
        grounded_in=ranked_info,
        mind_map_state=mind_map,
        goal="surface unknown unknowns"
    )
    
    # Step 3: Filter for novelty
    if is_redundant(question, discourse_history):
        return moderator_turn(...)  # Retry
    
    # Step 4: Polish
    return polish_utterance(question, style="curious non-expert")
```

### 6.6 Dynamic Mind Map

A tree-structured knowledge organizer: `M = (Concepts, Edges)`

**Operations:**

| Operation | Trigger | Action |
|-----------|---------|--------|
| **Insert** | New information discovered | Place under most relevant concept (semantic similarity + LLM selection) |
| **Reorganize** | Concept has > K pieces of info | Generate subtopics, redistribute info |
| **Cleanup** | Periodic | Remove empty concepts, collapse single-child nodes |

**Purpose:**
- Reduces cognitive load during long conversations
- Provides visual navigation of knowledge space
- Serves as outline for final report
- Interactive UI element (clickable, expandable)

```
Mind Map Example:
━━━━━━━━━━━━━━━━━━
Nuclear Energy in Saudi Arabia
├── Economic Factors
│   ├── Capital costs
│   ├── Operational savings
│   └── ROI timeline
├── Technical Requirements
│   ├── Infrastructure
│   ├── Workforce training
│   └── Technology partners
├── Environmental Impact
│   ├── Carbon reduction
│   └── Waste management
└── Geopolitical Considerations
    ├── Regional stability
    └── International agreements
```

### 6.7 Report Generation

When discourse concludes:

```python
def generate_report(mind_map, discourse_history, retrieved_sources):
    report = []
    
    for concept in mind_map.traverse_depth_first():
        section = generate_section(
            concept=concept,
            info=concept.associated_info,
            sources=retrieved_sources
        )
        # Every claim backed by citation
        section = add_citations(section, sources)
        report.append(section)
    
    return compile_report(report, style="wikipedia")
```

**Output:** Comprehensive, cited document tailored to user's exploration path.

### 6.8 Core Components

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Frontend** | Next.js / React | Real-time chat + mind map UI |
| **Discourse Manager** | FastAPI | Turn policy, initiative control |
| **Expert Agents** | Claude / GPT-4 | Perspective-driven responses |
| **Moderator Agent** | Claude / GPT-4 | Stagnation detection, redirection |
| **Retrieval Layer** | Bing/Tavily + RAG | Web search, document retrieval |
| **Mind Map Store** | Redis / PostgreSQL | Tree structure, real-time updates |
| **Database** | PostgreSQL | Users, sessions, reports |
| **Real-time** | WebSockets | Live streaming, user interjection |
| **Report Engine** | Markdown + PDF | Final deliverable generation |

---

## 7. User Interface

### 7.1 Main Screen — Discussion View

```
┌─────────────────────────────────────────────────────────────┐
│  ☰  Advisory Roundtable              [Save] [Share] [New]  │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  Topic: "Should we build or buy our AI infrastructure?"    │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ 👤 Dr. Tech CTO (Infrastructure)                    │   │
│  │ "Building in-house gives you full control, but the  │   │
│  │ talent acquisition alone takes 18-24 months..."     │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ 👤 Sarah Chen (Finance)                             │   │
│  │ "I'd push back on that timeline. The real question  │   │
│  │ is opportunity cost. While you're building, your    │   │
│  │ competitors are shipping with off-the-shelf..."     │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  ┌─────────────────────────────────────────────────────┐   │
│  │ 👤 Marcus (Enterprise Sales)                        │   │
│  │ "Both of you are missing the customer angle. I've   │   │
│  │ seen deals fall through because clients didn't      │   │
│  │ trust third-party AI handling their data..."        │   │
│  └─────────────────────────────────────────────────────┘   │
│                                                             │
│  ┌─ Panel ──────────────────────────────────────────────┐  │
│  │ [👤 CTO] [👤 Finance] [👤 Sales] [👤 Legal] [+ Add]  │  │
│  └──────────────────────────────────────────────────────┘  │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│  💬 Interject: [What about hybrid approach?        ] [Send]│
│                                                             │
│  Quick actions: [Challenge] [Redirect] [Consensus] [Wrap]  │
└─────────────────────────────────────────────────────────────┘
```

### 7.2 SME Panel Selection (Alternative Mode)

Allow users to optionally curate their own panel:
- Browse SME archetypes by domain
- Star/save favorite experts
- Create custom SME personas
- Import real people's public perspectives (LinkedIn, articles)

### 7.3 Mobile-First Design

- Swipeable expert cards
- Voice input for moderation
- Collapsible expert bios
- Share to WhatsApp/Twitter

---

## 8. Monetization

### 8.1 Freemium Model

| Tier | Price | Limits |
|------|-------|--------|
| **Free** | $0 | 3 discussions/month, 3 SMEs max, no export |
| **Pro** | $19/mo | Unlimited discussions, 5 SMEs, export, history |
| **Team** | $49/mo | Multi-user, shared discussions, custom SMEs |
| **Enterprise** | Custom | API access, private deployment, fine-tuned SMEs |

### 8.2 Additional Revenue

- **Custom SME training:** Upload documents to create domain-specific experts
- **API access:** Integrate roundtable into other products
- **White-label:** Branded version for consulting firms

---

## 9. Competitive Analysis

| Feature | Afyaa.net | Character.AI | ChatGPT/Claude | Co-STORM | **Our Platform** |
|---------|-----------|--------------|----------------|----------|------------------|
| Dynamic SME generation | ❌ Fixed | ❌ Fixed | ⚠️ Manual | ✅ Yes | ✅ Yes |
| Multi-expert discussion | ❌ Individual | ❌ 1:1 only | ❌ No | ✅ Yes | ✅ Yes |
| Mixed initiative | ❌ No | ❌ No | ❌ User-only | ✅ Yes | ✅ Yes |
| Auto-moderator | ❌ No | ❌ No | ❌ No | ✅ Yes | ✅ Yes |
| Live mind map | ❌ No | ❌ No | ❌ No | ✅ Yes | ✅ Yes |
| Cited report generation | ❌ No | ❌ No | ⚠️ Basic | ✅ Yes | ✅ Yes |
| Web retrieval per turn | ❌ No | ❌ No | ⚠️ Limited | ✅ Yes | ✅ Yes |
| Arabic-first | ✅ Yes | ❌ No | ⚠️ Secondary | ❌ No | ✅ Yes |
| Mobile-optimized | ⚠️ Basic | ✅ Yes | ✅ Yes | ❌ Web only | ✅ Yes |

**Our differentiation from Co-STORM:**
- Arabic-first with cultural context
- Mobile-native design
- Simpler onboarding (no Stanford research UI)
- Commercial product vs. research demo

---

## 10. MVP Scope (v1.0)

### Must Have (P0)
- [ ] Topic input → Dynamic SME panel generation (3-4 experts)
- [ ] Turn management: round-robin + user override
- [ ] Expert pipeline: intent selection → retrieval → response → polish
- [ ] Basic moderator: intervene after 3 stagnant turns
- [ ] Real-time streaming UI (chat format)
- [ ] Basic mind map display (read-only tree view)
- [ ] Session persistence
- [ ] Arabic + English support

### Should Have (P1)
- [ ] User accounts (OAuth)
- [ ] Interactive mind map (clickable, expandable)
- [ ] Report generation (Markdown export with citations)
- [ ] Mobile-responsive design
- [ ] Moderator pipeline (rerank unused info, generate novel questions)

### Nice to Have (P2)
- [ ] Custom SME creation/editing
- [ ] Mind map operations: reorganize, cleanup
- [ ] PDF report export
- [ ] Voice input
- [ ] Shareable discussion links
- [ ] Panel templates (e.g., "Startup Board", "Policy Review")

---

## 11. Success Metrics

| Metric | Target (3 months) |
|--------|-------------------|
| Monthly Active Users | 5,000 |
| Discussions created | 20,000 |
| Avg. discussion length | 8+ turns |
| User moderation rate | 60%+ inject at least once |
| Avg. turns before first intervention | 3-4 (per Co-STORM research) |
| Paid conversion | 5% |
| NPS | 50+ |

### Quality Metrics (from Co-STORM Evaluation)

| Metric | RAG Baseline | Target |
|--------|--------------|--------|
| Relevance | 3.57 | 3.75+ |
| Breadth | 3.50 | 3.75+ |
| Depth | 3.26 | 3.70+ |
| Novelty (unknown unknowns) | 2.44 | 3.00+ |

**Critical finding:** Moderator agent is essential — removing it causes 10% drop in depth, 5% drop in novelty.

---

## 12. Risks & Mitigations

| Risk | Impact | Mitigation |
|------|--------|------------|
| SMEs produce shallow/generic responses | High | Strong prompt engineering, retrieval augmentation |
| Discussion becomes repetitive | Medium | Diversity scoring, automatic topic evolution |
| High API costs per session | High | Caching, shorter context, cheaper models for drafts |
| Users expect real expert knowledge | Medium | Clear "AI simulation" disclaimer |
| Controversial topics → harmful content | High | Content moderation layer, topic guardrails |

---

## 13. Roadmap

### Phase 1: MVP (Weeks 1-6)
- Core discussion engine
- Basic web UI
- 3-expert panels
- Manual topic input

### Phase 2: Polish (Weeks 7-10)
- User accounts
- Session history
- Export features
- Mobile optimization

### Phase 3: Growth (Weeks 11-16)
- Custom SME creation
- Team features
- API launch
- Paid tiers

### Phase 4: Scale (Months 5+)
- Fine-tuned domain models
- Enterprise features
- White-label options
- Community SME marketplace

---

## 14. Open Questions

### Product
1. **Should SMEs have persistent memory across sessions?** (e.g., "As I mentioned in our last discussion...")
2. **Real names vs. synthetic personas?** (Legal/ethical considerations for using "Elon Musk" style names)
3. **How to handle controversial topics?** (Politics, religion — especially for Arabic market)
4. **Voice mode?** (Listen to experts "talk" to each other via TTS)
5. **Integration with real data?** (Pull user's documents, company data into context)

### Technical
6. **Build on knowledge-storm package or from scratch?** Co-STORM is MIT-licensed, could fork/adapt
7. **Search provider?** Bing API vs. Tavily vs. You.com for retrieval
8. **LLM cost optimization?** Each turn requires retrieval + generation — could get expensive
9. **Mind map persistence format?** JSON tree vs. graph DB
10. **Streaming architecture?** SSE vs. WebSockets for real-time discourse

### Localization
11. **Arabic retrieval quality?** Most search APIs are English-biased
12. **Expert names for Arabic market?** Should we include Arab business figures?
13. **RTL mind map rendering?** UI complexity for Arabic tree structures

---

## 15. References

### Academic Foundation
- **Co-STORM Paper:** Jiang, Y., Shao, Y., Ma, D., Semnani, S.J., & Lam, M.S. (2024). *"Into the Unknown Unknowns: Engaged Human Learning through Participation in Language Model Agent Conversations."* EMNLP 2024, pp. 9917–9955.
- **STORM Paper:** Shao, Y., et al. (2024). *"Assisting in Writing Wikipedia-like Articles From Scratch with Large Language Models."* NAACL 2024.

### Implementation Reference
- **Repository:** https://github.com/stanford-oval/storm
- **Live Demo:** https://storm.genie.stanford.edu
- **Python Package:** `pip install knowledge-storm`

### Key Source Files (for implementation reference)
| File | Purpose |
|------|---------|
| `knowledge_storm/collaborative_storm/engine.py` | Core engine with DiscourseManager |
| `knowledge_storm/collaborative_storm/modules/co_storm_agents.py` | LLM agent definitions |
| `knowledge_storm/collaborative_storm/modules/` | All customizable modules |

---

## 16. Appendix

### A. Sample Discussion Transcript

**Topic:** "How should a SaaS startup approach enterprise sales?"

**Panel:**
- Jason Lemkin (SaaS Expert)
- Jill Konrath (Sales Strategy)  
- David Skok (Venture/Metrics)

**[Opening Statements]**

**Jason:** "Enterprise sales is a different beast. You need to slow down to speed up. The biggest mistake I see is founders trying to close $100K deals with the same playbook they used for $1K self-serve..."

**Jill:** "Building on Jason's point — it's not just about slowing down, it's about expanding the buying committee. In enterprise, you're never selling to one person. Map the org chart before the first call..."

**David:** "Both valid, but let's talk unit economics. Before you even attempt enterprise, run the numbers. If your CAC payback exceeds 18 months without enterprise, you're not ready. The sales cycle will kill you..."

**[Moderator interjects]:** "What if we only have 2 salespeople?"

**Jason:** "Two salespeople for enterprise? That's actually fine for starting. But they need to be the RIGHT two. I'd rather have one great enterprise AE than five mediocre ones..."

---

### B. Technical Glossary

- **SME:** Subject Matter Expert
- **Orchestrator:** Backend service managing discussion flow
- **Context window:** Token limit for LLM conversation history
- **Moderation injection:** User prompt inserted mid-discussion

---

*Document ends.*
