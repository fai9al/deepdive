# DeepDive 🌊

**AI-Augmented Consultation Platform for Expert Advisory Work**

> Not human alone. Not AI alone. Both working together.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Inspired by Co-STORM](https://img.shields.io/badge/Inspired%20by-Stanford%20Co--STORM-blue)](https://github.com/stanford-oval/storm)

---

## 🎯 The Problem

Every organization — public or private — has the same problem:

> **They have senior employees they call "experts." But those experts cannot deliver their consultation in a proper way.**

These experts have decades of experience. Deep knowledge. Institutional context. But:
- Their expertise stays **trapped in their heads**
- Their output is **inconsistent** — rambling emails, unstructured docs
- They **miss angles** they don't know to consider
- They **can't format** to MBB/executive standards

## 💡 The Solution

DeepDive bridges the **expertise delivery gap**:

```
Expert Knowledge  →  AI-Guided Discussion  →  Structured Deliverable
   (in their head)    (surfaces everything)     (MBB-quality output)
```

> *"Not human alone. Not AI alone. Both working together."*

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🎭 **Dynamic SME Generation** | Experts are synthesized based on your topic, not pre-built personas |
| 💬 **Autonomous Discussion** | SMEs respond to each other, not just to you |
| 🎛️ **Mixed Initiative** | Observe passively OR actively moderate the discourse |
| 🗺️ **Live Mind Map** | Hierarchical knowledge organization updated in real-time |
| 📄 **Cited Reports** | Generate Wikipedia-style documents with sources |
| 🌍 **Arabic-First** | Built for Arabic + English from day one |

---

## 🔄 How It Works

```
┌─────────────────────────────────────────────────────────────┐
│                         DeepDive                            │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│   1. Enter your topic or question                           │
│                    ↓                                        │
│   2. System generates 3-5 relevant experts                  │
│                    ↓                                        │
│   3. Experts discuss autonomously (round-robin)             │
│                    ↓                                        │
│   4. You can inject prompts anytime to steer                │
│                    ↓                                        │
│   5. Moderator intervenes if discussion stagnates           │
│                    ↓                                        │
│   6. Mind map organizes discovered knowledge                │
│                    ↓                                        │
│   7. Generate final cited report                            │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 🏗️ Architecture

### System Participants

```
┌──────────────┐   ┌──────────────┐   ┌──────────────────┐
│    Human     │   │  Moderator   │   │  LLM Expert(s)   │
│    User      │◄──┤    Agent     │◄──┤   (N experts)    │
└──────┬───────┘   └──────┬───────┘   └──────────────────┘
       │                  │
       └────────┬─────────┘
                ▼
       ┌─────────────────┐
       │    Discourse    │
       │    Manager      │
       └────────┬────────┘
                ▼
       ┌─────────────────┐
       │  Dynamic Mind   │
       │   Map Engine    │
       └────────┬────────┘
                ▼
       ┌─────────────────┐
       │     Report      │
       │    Generator    │
       └─────────────────┘
```

### Turn Management Rules

1. **Warm-up:** N experts each take one opening turn
2. **Round-robin:** Experts take turns sequentially  
3. **Moderator intervention:** After L consecutive answer-only turns, moderator injects new direction
4. **User override:** User can inject at ANY time
5. **Return to auto:** After user input, system resumes auto-steering

---

## 📊 Comparison

| Feature | ChatGPT | afyaa.net | Co-STORM | **DeepDive** |
|---------|---------|-----------|----------|--------------|
| Dynamic SME generation | ⚠️ Manual | ❌ Fixed | ✅ Yes | ✅ Yes |
| Multi-expert discussion | ❌ No | ❌ Individual | ✅ Yes | ✅ Yes |
| Mixed initiative | ❌ User-only | ❌ No | ✅ Yes | ✅ Yes |
| Auto-moderator | ❌ No | ❌ No | ✅ Yes | ✅ Yes |
| Live mind map | ❌ No | ❌ No | ✅ Yes | ✅ Yes |
| Arabic-first | ⚠️ Secondary | ✅ Yes | ❌ No | ✅ Yes |
| Mobile-optimized | ✅ Yes | ⚠️ Basic | ❌ Web only | ✅ Yes |

---

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ or Python 3.10+
- OpenAI/Anthropic API key
- Search API key (Bing/Tavily/You.com)

### Installation

```bash
# Clone the repo
git clone https://github.com/fai9al/deepdive.git
cd deepdive

# Install dependencies
npm install  # or pip install -r requirements.txt

# Configure API keys
cp .env.example .env
# Edit .env with your keys

# Run
npm run dev  # or python main.py
```

---

## 📖 Documentation

- [Product Requirements Document (PRD)](docs/PRD.md)
- [Co-STORM Reference](docs/references/co-storm-documentation.md)
- [Architecture Deep Dive](docs/architecture.md) *(coming soon)*
- [API Reference](docs/api.md) *(coming soon)*

---

## 🗺️ Roadmap

### Phase 1: MVP (Weeks 1-6)
- [ ] Topic input → Dynamic SME panel generation
- [ ] Turn management: round-robin + user override
- [ ] Expert pipeline: intent → retrieval → response → polish
- [ ] Basic moderator intervention
- [ ] Real-time streaming UI
- [ ] Basic mind map display
- [ ] Arabic + English support

### Phase 2: Polish (Weeks 7-10)
- [ ] User accounts
- [ ] Interactive mind map
- [ ] Report generation with citations
- [ ] Mobile optimization

### Phase 3: Growth (Weeks 11-16)
- [ ] Custom SME creation
- [ ] Team features
- [ ] API launch
- [ ] Paid tiers

---

## 🔬 Research Foundation

DeepDive is inspired by **Co-STORM** from Stanford's OVAL Lab (EMNLP 2024):

> Jiang, Y., Shao, Y., Ma, D., Semnani, S.J., & Lam, M.S. (2024). *"Into the Unknown Unknowns: Engaged Human Learning through Participation in Language Model Agent Conversations."*

Key research findings we're building on:
- **Moderator is critical:** Removing it causes 10% drop in depth, 5% drop in novelty
- **User behavior:** People observe 3-4 turns before first intervention
- **Unknown unknowns:** Users discover information they didn't know to ask about

---

## 🤝 Contributing

Contributions welcome! Please read our [Contributing Guide](CONTRIBUTING.md) first.

```bash
# Fork the repo
# Create your feature branch
git checkout -b feature/amazing-feature

# Commit your changes
git commit -m 'Add amazing feature'

# Push to the branch
git push origin feature/amazing-feature

# Open a Pull Request
```

---

## 📜 License

MIT License — see [LICENSE](LICENSE) for details.

---

## 🙏 Acknowledgments

- [Stanford OVAL Lab](https://oval.cs.stanford.edu/) for Co-STORM research
- [STORM Project](https://github.com/stanford-oval/storm) for the foundation

---

<p align="center">
  <strong>Built with 🤖 by Dr. Faisal Alotaibi</strong>
</p>
