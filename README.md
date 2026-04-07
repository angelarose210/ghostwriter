# Ghostwriter

**AI agent skills that learn how you write — then write like you.**

Feed it your writing samples and Ghostwriter reverse-engineers your voice into a reusable profile: your sentence rhythms, vocabulary choices, tone, quirks — all of it. Then it applies that profile to anything the agent writes for you, so the output actually sounds like *you* wrote it.

No more "as an AI" energy. No more corporate filler. Just your voice, at scale.

Ships with a comprehensive **AI writing tells database** (200+ banned words, phrases, sentence patterns, and formatting habits) so everything it writes passes as genuinely human.

Works with **Claude Code**, **Hermes Agent**, and **OpenClaw** out of the box.

---

## See it in action

Here's a typical LinkedIn post about making money with AI. The first version is what you get when you ask ChatGPT to write it. The second is what Ghostwriter produces.

### Before: Raw AI output

> **Last Tuesday at 3:47 AM, I finally cracked the code on my AI income system. After 47 days of testing 12 different models across ChatGPT-5.4, Claude 4.6, and Gemini 3.1, I've built something that's completely changed my trajectory. 🚀**
>
> Here's the exact framework that's generated $470 in passive income this week alone:
>
> **1. 🤖 Leverage multimodal LLMs for async content production.** By orchestrating GPT-5.4's function calling with Claude's artifact generation, I created a 73% reduction in manual copywriting overhead while maintaining semantic coherence across my brand touchpoints.
>
> **2. 🤝 Deploy conversational agents for intent-based lead scoring.** My custom chatbot (built in 2.3 hours using Python, LangChain, and a $19/mo OpenAI API key) now processes 23.7 qualified conversations daily — a 340% improvement from my previous manual workflow.
>
> **3. 🧠 Productize your infrastructure as a high-ticket service offering.** I'm now packaging this exact system into a $497 white-glove implementation for my LinkedIn network. Already closed 3 clients ($1,491 ARR) with 2 more in pipeline.
>
> The ROI? 23.6x return on tool costs in Week 1 alone.
>
> It's not about replacing human ingenuity. It's about augmenting your cognitive bandwidth with compound leverage. ✨
>
> What systems are YOU building with AI this quarter? I'd love to connect with other operators in the comments. 👇
>
> #AI #MachineLearning #DigitalTransformation #ChatGPT #PassionToProfit #Entrepreneurship #FutureOfWork #BuildInPublic

**AI tells in this post:** Fake specificity (3:47 AM, 47 days, 12 models, 2.3 hours, $19/mo, 23.7 conversations, 340%, $1,491 ARR, 23.6x ROI, Week 1), unnecessary precision on made-up numbers, jargon stacking ("multimodal LLMs," "async content production," "semantic coherence," "intent-based lead scoring," "cognitive bandwidth," "compound leverage"), acronym dropping (ARR, ROI, LLM), fake scarcity ("cracked the code," "completely changed"), LinkedIn optimization bait ("connect with other operators"), metric theater (percentages that don't mean anything), objective correlatives ("trajectory," "pipeline"), framework naming without substance, the It's-Not-X-It's-Y negation pattern, emoji bullet decoration. This hits specificity-without-substance — lots of numbers that create faux authority but say nothing about what actually happened.

### After: Ghostwriter output

> $4,200 extra last month from AI tools I barely knew existed six months ago.
>
> No course. No "method." Just paid attention to what was moving numbers and ignored the hype threads.
>
> Three things in my stack:
>
> **Ghostwriting myself.** I feed AI my past emails, proposals, project notes. It drafts in my voice. 10 minutes of edits vs. an hour writing from scratch.
>
> **Brutal lead qualification.** Chatbot asks five questions, auto-scores, only sends me the ones that pass. Built it in an afternoon. Saves ~6 hours/week of convos with non-buyers.
>
> **Selling the setup.** Small biz owners know they "should be using AI" but have no clue where to start. $500 to get them running. Takes me about 3 hours now that I've templated it.
>
> Tools are free or cheap. The friction is just sitting down and building instead of reading another thread about how AI will change everything.
>
> What's actually working in your stack? Genuinely curious — not engagement farming.

**This voice tells you:** Specific numbers ($4,200, 6 hours/week, 3 hours), stack/stack-based language, "ghostwriting myself" (self-referential clarity), timeframe qualifiers ("now that I've templated it"), cost-conscious framing ("free or cheap"), production vs. consumption contrast, genuine question with explicit non-bait disclaimer. Plus: no emojis, no bold-first bullet points, variable sentence length, short opener, no throat-clearing.

---

## What's in the box

Ghostwriter is a set of four skills that work together:

| Skill | What it does |
| --- | --- |
|**voice-analyze**|Feed it writing samples, it extracts a voice profile — sentence length patterns, vocabulary, tone markers, the works|
|**voice-create**|Describe the voice you want in plain English and it generates a profile from scratch|
|**voice-blend**|Mix two or more voice profiles together with custom ratios (e.g., 70% your blog voice / 30% technical docs)|
|**voice-apply**|Apply any voice profile to transform content — rewrites, new drafts, tone shifts|

## The AI tells engine

This is what makes Ghostwriter different from "just use a custom prompt." Every skill is built on top of a reference database (`references/ai-tells.md`) that catalogs the specific patterns that make AI writing detectable:

**Banned vocabulary (200+ words):** The verbs, adjectives, nouns, and adverbs that AI models reach for constantly. Words like "delve," "leverage," "multifaceted," "tapestry," "furthermore." If a word shows up in 10x more AI text than human text, it's on the list.

**Banned sentence structures:** The "It's not X, it's Y" negation flip (the single most prominent AI tell). Self-posed questions answered immediately. Anaphora abuse. Present participle trailing clauses like "highlighting its importance."

**Banned transitions:** Throat-clearing openers ("In today's digital age"), pedagogical bot-voice ("Let's dive in!"), fake suspense ("Here's the thing"), hype phrases ("game-changer"), and formulaic closers ("In conclusion").

**Punctuation rules:** Em dashes are the #1 AI punctuation tell (AI uses \~10x more than humans). Ghostwriter replaces them with commas, periods, parentheses, or colons. Same treatment for semicolons and Oxford commas unless the user naturally uses them.

**Rhythm enforcement:** AI sentences cluster at 15-20 words. Humans swing from 3-word fragments to 40-word sprawls. Ghostwriter enforces high variance in sentence and paragraph length, breaks the Rule of Three when it appears back-to-back, and varies subsection lengths.

**Formatting tells:** No bold-first bullet points. No erratic bolding. No excessive headers. No emoji in professional contexts.

**Tone guards:** No relentless positivity, no false balance, no emotional flatness, no elevated register for simple ideas.

Every skill uses these rules differently:

* **voice-analyze** scans your samples for AI tells and reports what it finds
* **voice-create** bakes the avoidance rules into every new profile automatically
* **voice-blend** treats AI tell avoidance as a hard constraint that can't be blended away
* **voice-apply** runs a mandatory elimination pass on all output before delivering it

## Quick start

### 1\. Install

Clone the repo or just give the repo url to your agent to install:

```bash
git clone https://github.com/angelarose210/ghostwriter-skills.git
```

Then copy the skills for your agent:

**Claude Code:**

```bash
cp -r ghostwriter-skills/.claude/skills/voice-\* your-project/.claude/skills/
```

**Hermes Agent:**

```bash
cp -r ghostwriter-skills/.hermes/skills/voice-\* your-project/.hermes/skills/
```

**OpenClaw:**

```bash
cp -r ghostwriter-skills/.openclaw/skills/voice-\* your-project/.openclaw/skills/
```

Or just clone the whole repo and work inside it — your agent will pick up the skills automatically from the matching directory.

### 2\. Analyze your writing

Paste some of your writing into the chat and say:

```
Analyze this writing style and create a voice profile
```

Ghostwriter will break down your:

* Sentence structure and length patterns
* Vocabulary complexity and domain
* Tone (formality, confidence, warmth, energy)
* Structural habits (lists, examples, questions)
* Perspective and voice choices

It outputs a YAML voice profile you can reuse anywhere.

### 3\. Write in your voice

Once you have a profile, just say:

```
Write release notes in my voice
```

```
Rewrite this email to sound like me
```

```
Draft a blog post using the brand-voice profile
```

## Compatibility

This repo ships the same four skills in three directory formats so they work everywhere:

| Agent | Skills directory | Format notes |
| --- | --- | --- |
| **Claude Code** | `.claude/skills/` | Standard AgentSkills spec |
| **Hermes Agent** | `.hermes/skills/` | Same spec, different path |
| **OpenClaw** | `.openclaw/skills/` | Adds `metadata.openclaw` block in frontmatter for gating |

The skill logic is identical across all three. The only differences are the directory name and minor frontmatter fields that each agent expects.

### AgentSkills standard

All three formats follow the [AgentSkills](https://agentskills.io) convention:

* YAML frontmatter with `name`, `description`, `version`
* Markdown body with instructions
* Optional `scripts/`, `references/`, and `assets/` subdirectories

## How the voice profiles work

Each profile captures five dimensions on a 0-1 scale:

| Dimension | Low (0) | High (1) |
| --- | --- | --- |
| **Formality** | Casual, contractions, fragments | Formal, complete sentences, no contractions |
| **Confidence** | Hedging, qualifiers, "might/perhaps" | Direct, assertive, conclusions first |
| **Warmth** | Clinical, third-person, detached | Friendly, "you/we", empathetic |
| **Energy** | Calm, measured, understated | Dynamic, exclamation points, action verbs |
| **Complexity** | Short sentences, simple words | Long sentences, technical vocabulary |

Beyond the five dimensions, profiles also capture:

* **Vocabulary preferences** — words to use and avoid
* **Signature phrases** — your recurring patterns and constructions
* **Structure patterns** — paragraph length, list usage, example frequency
* **Perspective** — first/second/third person, active/passive voice

### Example profile output

```yaml
name: my-writing-voice
version: 1.0.0
description: Voice profile extracted from blog posts
analysis\_source:
  sample\_size: 2400
  sample\_count: 5
  confidence: 0.88
tone:
  formality: 0.3
  confidence: 0.75
  warmth: 0.8
  energy: 0.65
  complexity: 0.45
vocabulary:
  prefer:
    - "here's the thing"
    - "in practice"
    - "the real question is"
  avoid:
    - "utilize"
    - "leverage"
    - "synergy"
  signature\_phrases:
    - "Let me break this down..."
    - "The short version:"
structure:
  sentence\_length: medium
  paragraph\_length: short
  sentence\_variety: high
  use\_lists: when-appropriate
  use\_examples: frequently
  use\_questions: frequently
perspective:
  person: first
  voice: active
  tense: present
```

## Usage examples

### Extract your voice from samples

Paste your writing (blog posts, emails, docs — 500+ words works best, 3+ samples is ideal):

```
Here are three of my recent blog posts. Analyze the writing style
and create a voice profile called "my-blog-voice":

\[paste your writing here]
```

### Create a voice from a description

Don't have samples? Describe what you want:

```
Create a voice profile for developer docs — direct, no hand-holding,
assumes the reader knows what they're doing. Technical but not stuffy.
Skip the "in this tutorial you will learn" stuff.
```

### Blend voices

Mix profiles with custom ratios:

```
Blend my-blog-voice and technical-authority — 70/30
```

```
Combine executive-brief and casual-conversational equally
```

### Apply a voice to content

```
Rewrite this support doc in the friendly-explainer voice
```

```
This email sounds too stiff — dial the formality down 30%
```

```
Write a changelog entry using my-blog-voice
```

## Built-in voice templates

Four starter profiles are included so you can use Ghostwriter immediately:

| Profile | Tone | Good for |
| --- | --- | --- |
| `technical-authority` | Direct, precise, confident | Architecture docs, API references, engineering specs |
| `friendly-explainer` | Warm, encouraging, accessible | Tutorials, onboarding, README files |
| `executive-brief` | Concise, outcome-focused, strategic | Board decks, stakeholder updates, business cases |
| `casual-conversational` | Relaxed, personal, energetic | Blog posts, newsletters, social media |

Use them as-is, blend them, or use them as starting points for your own profiles.

## Where profiles are stored

| Location | Scope |
| --- | --- |
| `.aiwg/voices/` | Project-specific (committed to repo) |
| `~/.config/aiwg/voices/` | User-wide (shared across projects) |

## Tips for better voice profiles

1. **More samples = better profiles.** Three 500-word samples beats one 1500-word sample.
2. **Keep the genre consistent.** Don't mix your tweets with your whitepapers in the same analysis.
3. **Check the confidence score.** Anything above 0.8 is solid. Below 0.6, feed it more samples.
4. **Iterate.** Analyze, apply, compare to the original, adjust. The blend feature is great for fine-tuning.
5. **Name your profiles well.** `blog-voice-casual` is more useful than `my-voice-2` six months later.

## Requirements

* One of: [Claude Code](https://docs.anthropic.com/en/docs/claude-code), [Hermes Agent](https://github.com/hermes-agent), or [OpenClaw](https://github.com/openclaw)
* That's it. No dependencies, no API keys, no build step.

## File structure

```
ghostwriter-skills/
  .claude/skills/          # Claude Code
    voice-analyze/SKILL.md
    voice-apply/
      SKILL.md
      references/
        ai-tells.md        # AI writing tells database (the secret sauce)
    voice-create/SKILL.md
    voice-blend/SKILL.md
  .hermes/skills/          # Hermes Agent (same structure)
    voice-analyze/SKILL.md
    voice-apply/
      SKILL.md
      references/ai-tells.md
    voice-create/SKILL.md
    voice-blend/SKILL.md
  .openclaw/skills/        # OpenClaw (same structure, metadata frontmatter)
    voice-analyze/SKILL.md
    voice-apply/
      SKILL.md
      references/ai-tells.md
    voice-create/SKILL.md
    voice-blend/SKILL.md
  README.md
  LICENSE
```

## Contributing

If another agent framework adopts the AgentSkills spec, adding support is straightforward — create a new dotfile directory with the same SKILL.md files and adjust the frontmatter to match. PRs welcome.

## License

MIT — do whatever you want with it.

\---

Built by [Angela Ai Specialist](https://www.facebook.com/profile.php?id=61574356028671) for people who are tired of AI writing that sounds like AI writing.

Join the [Facebook group](https://www.facebook.com/groups/814195164542542) for tips, new voice profiles, and updates.

#   g h o s t w r i t e r  
 