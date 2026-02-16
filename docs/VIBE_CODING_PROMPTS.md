# DeepDive — Vibe Coding Prompts

Step-by-step prompts for building DeepDive with Lovable, GPT-Engineer, or similar tools.

---

## Pre-Session Setup

Before starting, have ready:
- OpenAI or Anthropic API key
- The PRD open for reference
- A real consultation topic to test with

---

## Session 1: The Discussion Engine

**Goal:** Get AI perspectives talking to each other on any topic.

### Prompt 1.1 — Project Setup

```
Create a new React app with TypeScript and Tailwind CSS.

The app is called "DeepDive" — an AI consultation platform where domain experts get help covering all aspects of a topic through multi-perspective AI discussion.

Set up:
- Vite + React + TypeScript
- Tailwind CSS with RTL support (Arabic)
- A clean, professional UI (think consulting firm aesthetic)
- Dark mode support
- Mobile responsive

Create a home page with:
- App title "DeepDive" with Arabic subtitle "الغوص العميق"
- Tagline: "Not human alone. Not AI alone. Both working together."
- A large text input for entering a consultation topic
- A "Start Discussion" button
```

### Prompt 1.2 — Perspective Generation

```
When the user enters a topic and clicks "Start Discussion":

1. Call an LLM API (OpenAI or Anthropic) to generate 3-4 expert perspectives relevant to THIS specific topic.

2. Each perspective should have:
   - Name (realistic, professional)
   - Title/Role
   - Expertise area
   - A short 1-line description of their angle
   - An avatar (use initials or a placeholder)

3. Display the generated panel as cards before starting the discussion.

4. Add a "Begin Discussion" button to proceed.

Example for topic "Digital transformation for healthcare":
- Dr. Sarah Chen, Healthcare IT Director — "EHR systems and interoperability"
- Ahmed Al-Hassan, Change Management Lead — "Workforce adoption and training"
- Prof. James Miller, Health Policy Expert — "Regulatory compliance and patient privacy"

The perspectives should be DIVERSE — different angles, not all agreeing.
```

### Prompt 1.3 — Discussion Flow

```
Create the discussion interface:

1. Chat-style layout with messages from each perspective
2. Each message shows: avatar, name, role, and their response
3. Visual distinction between different speakers (subtle color coding)

Discussion flow:
1. Each perspective gives an opening statement (round 1)
2. Then round-robin: each perspective responds to what others said
3. They should reference each other: "Building on what Sarah said..." or "I'd push back on Ahmed's point..."
4. Run for 3 rounds automatically

Technical:
- Stream responses in real-time (show typing indicator)
- Each turn calls the LLM with full conversation history
- Include the perspective's role/angle in the system prompt
- Responses should be 2-3 paragraphs max

UI:
- Auto-scroll to latest message
- Show "Discussion in progress..." between turns
- Add a "Pause Discussion" button
```

### Prompt 1.4 — User Interjection

```
Add the ability for the user (the expert) to interject:

1. Always-visible input bar at the bottom: "Interject in the discussion..."
2. When user submits, their message appears in the chat with a distinct style (highlighted, labeled "You" or "Expert")
3. The discussion PAUSES
4. The next perspective responds directly to the user's input
5. Then discussion continues from there

The user might:
- Ask for clarification: "Can you elaborate on the regulatory aspect?"
- Redirect: "Let's focus on the budget implications"
- Correct: "Actually, cloud is not an option for this client"
- Challenge: "I disagree — what about X?"

All perspectives should acknowledge and incorporate the user's input.
```

### Prompt 1.5 — Basic Moderator

```
Add a Moderator agent that intervenes when discussion stagnates:

1. Track the discussion: if 3 consecutive turns are just answers/agreements without new questions or challenges...
2. The Moderator interjects with a thought-provoking question
3. Moderator style: "curious non-expert" — asks the questions the user might not think to ask

Moderator appears differently in UI:
- No avatar, or a special "Moderator" badge
- Message styled differently (maybe italic or subtle background)
- Example: "One area we haven't explored: How will this affect the existing vendor relationships?"

The Moderator's job is to surface UNKNOWN UNKNOWNS — things no one has mentioned yet.
```

---

## Session 2: Knowledge Organization

**Goal:** Track what's been discussed and identify gaps.

### Prompt 2.1 — Mind Map Data Structure

```
As the discussion progresses, build a mind map data structure:

1. Tree structure with the main topic as root
2. Each major theme becomes a branch
3. Sub-points nest under themes
4. Track which points have been discussed vs. identified but not explored

Data model:
{
  topic: "Digital transformation for healthcare",
  nodes: [
    {
      id: "1",
      label: "Technical Infrastructure",
      children: [
        { id: "1.1", label: "EHR Integration", status: "discussed" },
        { id: "1.2", label: "Cloud vs On-premise", status: "discussed" },
        { id: "1.3", label: "Data Migration", status: "gap" }
      ]
    },
    ...
  ]
}

After each discussion turn, call the LLM to:
- Extract key topics/points mentioned
- Categorize under existing nodes or create new ones
- Mark as "discussed" or "mentioned but not explored"
```

### Prompt 2.2 — Mind Map UI

```
Add a collapsible side panel showing the mind map:

1. Tree view with expand/collapse
2. Visual indicators:
   - ✓ Green: Discussed thoroughly
   - ◐ Yellow: Mentioned but shallow
   - ○ Red/Empty: Gap identified but not discussed
3. Clicking a node could prompt: "Explore this topic?"
4. Real-time updates as discussion progresses

Position: Right sidebar, collapsible
Style: Clean, minimal, professional
```

### Prompt 2.3 — Gap Identification

```
Enhance the Moderator to use the mind map:

1. Moderator sees the mind map state
2. Prioritizes questions about "gap" nodes
3. Explicitly calls out: "I notice we haven't discussed [X] yet. How does that factor in?"

Also add a "Gaps" summary section:
- Shows list of unexplored areas
- User can click to direct discussion there
- Gaps reduce as discussion covers them
```

### Prompt 2.4 — Session Persistence

```
Add ability to save and resume sessions:

1. Auto-save to localStorage every few turns
2. "Save Session" button → generates a session ID
3. "Load Session" on home page
4. Session includes:
   - Topic
   - Generated perspectives
   - Full discussion transcript
   - Mind map state

Optional: Add backend persistence (Supabase or similar) for sharing across devices.
```

---

## Session 3: Report Generation

**Goal:** Turn the discussion into a deliverable Markdown report.

### Prompt 3.1 — Report Generation Trigger

```
Add a "Generate Report" button that appears:
1. After at least 2 rounds of discussion
2. Or when user clicks "End Discussion"

The button should be prominent but not intrusive.
Also add: "Continue Discussion" option alongside it.
```

### Prompt 3.2 — Report Structure

```
When "Generate Report" is clicked:

1. Call the LLM with:
   - Full discussion transcript
   - Mind map structure
   - Instructions to generate a structured report

2. Report format:

# [Topic Title]

## Executive Summary
[2-3 paragraphs synthesizing the key findings and recommendations]

## 1. [First Major Theme from Mind Map]

### 1.1 [Subtopic]
[Content from discussion, synthesized and polished]
- Key point
- Supporting detail

### 1.2 [Subtopic]
...

## 2. [Second Major Theme]
...

## Recommendations
1. [Specific, actionable recommendation]
2. [Specific, actionable recommendation]
3. [Specific, actionable recommendation]

## Areas for Further Exploration
- [Gaps that weren't fully addressed]
- [Questions that remain open]

## Appendix: Sources & Discussion Summary
- Summary of perspectives consulted
- Key points of agreement/disagreement

3. Display the report in a clean reading view
4. Add "Export as Markdown" button
```

### Prompt 3.3 — Report Review Interface

```
Create a review interface for the generated report:

1. Side-by-side or tabbed view:
   - Left: The discussion transcript
   - Right: The generated report

2. For each section of the report, show:
   - The content
   - A subtle "Edit" button
   - A "This needs more discussion" button

3. If user clicks "Needs more discussion":
   - Return to discussion mode
   - The selected section becomes the focus
   - Perspectives address that specific gap

4. Add overall actions:
   - "Approve & Export" → Download .md file
   - "Continue Discussion" → Back to chat
   - "Regenerate Report" → Try again with same content
```

### Prompt 3.4 — Export & Polish

```
Finalize the export functionality:

1. "Export as Markdown" → Downloads .md file
   - Clean filename: "deepdive-[topic-slug]-[date].md"
   
2. Add copy-to-clipboard button

3. Polish the UI:
   - Loading states during generation
   - Success confirmations
   - Error handling

4. Add a "Start New Consultation" button to begin fresh
```

---

## Session 4 (Optional): Polish & Arabic

### Prompt 4.1 — Arabic Language Support

```
Add full Arabic support:

1. Language toggle (AR/EN) in header
2. When Arabic selected:
   - UI switches to RTL
   - All interface text in Arabic
   - Perspectives discuss in Arabic
   - Report generated in Arabic

3. The LLM prompts should specify the language

4. Arabic perspective names should be realistic Arabic names

Test with a real Arabic topic to verify quality.
```

### Prompt 4.2 — Visual Polish

```
Polish the overall UI:

1. Add subtle animations:
   - Messages fade in
   - Mind map nodes animate on update
   - Smooth transitions between views

2. Better typography:
   - Professional font pairing
   - Good hierarchy
   - Readable line lengths

3. Empty states:
   - When no discussion yet
   - When mind map is empty

4. Loading states:
   - Skeleton screens
   - Progress indicators

5. Mobile responsive:
   - Collapsible panels
   - Touch-friendly inputs
   - Readable on phone screens
```

---

## Testing Topics

Use these real consultation topics to test:

1. **"Digital transformation roadmap for a government ministry"**
   - Tests: Technical, change management, budget, policy perspectives

2. **"AI governance framework for a financial institution"**
   - Tests: Technical, regulatory, risk, ethics perspectives

3. **"Post-merger integration strategy"**
   - Tests: Operations, HR, culture, finance perspectives

4. **"Cybersecurity maturity assessment"**
   - Tests: Technical, compliance, training, incident response perspectives

5. **"Smart city initiative planning"**
   - Tests: Infrastructure, citizen services, privacy, sustainability perspectives

---

## Tips for Vibe Coding

1. **One prompt at a time** — Don't paste everything at once
2. **Test after each prompt** — Make sure it works before moving on
3. **Screenshot working states** — Reference for next session
4. **Keep the conversation going** — If something breaks, describe what happened
5. **Real data > test data** — Use actual consultation topics
6. **Deploy frequently** — Always have a working URL to share
7. **Paste PRD sections as context** — When the AI needs background

---

## Reference

- Full PRD: [docs/PRD.md](./PRD.md)
- Co-STORM Research: [docs/references/co-storm-documentation.md](./references/co-storm-documentation.md)
- GitHub: https://github.com/fai9al/deepdive

---

*Happy building! 🚀*
