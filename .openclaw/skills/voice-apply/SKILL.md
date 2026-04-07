---
name: voice-apply
description: "Applies a voice profile to transform content. Use when user asks to write in a specific voice, match a tone, apply a style, or transform content to sound like a particular voice profile."
version: 1.0.0
platforms: [all]
metadata: { "openclaw": { "requires": {} } }

---

# Voice Apply Skill

## Purpose

Transform content to match a specified voice profile. This skill loads voice profiles and applies their characteristics (tone, vocabulary, structure, perspective) to new or existing content.

**Critical rule**: Every piece of output MUST pass the AI writing tells check defined in `references/ai-tells.md`. This is non-negotiable. If the output contains any banned vocabulary, structures, transitions, or punctuation patterns from that reference, rewrite until clean.

## When This Skill Applies

- User asks to "write in X voice" or "use Y tone"
- User wants to "make this sound more [casual/formal/technical/etc.]"
- User provides content and asks to transform its style
- User references a voice profile by name
- User wants content to match a specific audience or context

## Trigger Phrases

| Natural Language | Action |
|------------------|--------|
| "Write this in technical voice" | Apply technical-authority profile |
| "Make it more casual" | Apply casual-conversational or calibrate toward casual |
| "This needs to sound executive" | Apply executive-brief profile |
| "Explain like I'm a beginner" | Apply friendly-explainer profile |
| "Use the [profile-name] voice" | Load and apply named profile |
| "Transform this to match [example]" | Analyze example, apply derived voice |

## Voice Profile Locations

Skill checks these locations (in order):
1. Project: `.aiwg/voices/`
2. User: `~/.config/aiwg/voices/`
3. Built-in: `voice-framework/voices/templates/`

## Built-in Voice Profiles

| Profile | Description | Best For |
|---------|-------------|----------|
| `technical-authority` | Direct, precise, confident | Docs, architecture, engineering |
| `friendly-explainer` | Approachable, encouraging | Tutorials, onboarding, education |
| `executive-brief` | Concise, outcome-focused | Business cases, stakeholder comms |
| `casual-conversational` | Relaxed, personal | Blog posts, social, newsletters |

## Application Process

### 1. Load Voice Profile

```python
# Load from YAML
profile = load_voice_profile("technical-authority")
```

### 2. Analyze Source Content (if transforming)

- Current tone characteristics
- Vocabulary patterns
- Structure patterns
- Gap analysis vs target voice

### 3. Apply Voice Characteristics

**Tone Calibration**:
- Adjust formality level (word choice, contractions)
- Calibrate confidence (hedging vs assertion)
- Set warmth (clinical vs personable)
- Tune energy (measured vs enthusiastic)

**Vocabulary Transformation**:
- Replace words per `prefer`/`avoid` guidance
- Introduce domain terminology naturally
- Weave in signature phrases where appropriate

**Structure Adjustment**:
- Modify sentence length distribution
- Adjust paragraph breaks
- Add/remove lists, examples, analogies as specified

**Perspective Shift**:
- Adjust narrative person (I, we, you, they)
- Calibrate opinion expression
- Set reader relationship tone

### 4. AI Tells Elimination Pass (MANDATORY)

After applying the voice profile, run every piece of output through the full AI tells check. This is the most important step. Reference: `references/ai-tells.md`

**Vocabulary check**: Scan output for every word in the banned lists:
- Banned verbs: delve, leverage, utilize, harness, unlock, unleash, empower, facilitate, foster, bolster, optimize, streamline, navigate, spearhead, underscore, illuminate, elucidate, embark, unravel, elevate, reimagine, revolutionize, transcend, resonate, showcase, craft, embrace, thrive, unveil, champion, and all others on the list
- Banned adjectives: multifaceted, seamless, robust, comprehensive, cutting-edge, holistic, meticulous, groundbreaking, transformative, innovative, compelling, invaluable, paramount, unprecedented, impactful, game-changing, and all others on the list
- Banned nouns: tapestry, realm, testament, beacon, myriad, landscape, ecosystem, paradigm, nexus, catalyst, synergy, roadmap, cornerstone, bedrock, pinnacle, plethora, stakeholders, and all others on the list
- Banned adverbs: furthermore, moreover, additionally, notably, crucially, importantly, consequently, seamlessly, fundamentally, undoubtedly, and all others on the list

**Transition check**: Remove all banned transitions:
- Throat-clearing: "in today's digital age", "in a world where", "when it comes to"
- Pedagogical: "let's dive in", "let's unpack this", "great question!"
- Signposting: "it's important to note", "it's worth noting", "this underscores"
- Fake-suspense: "here's the thing", "the best part?", "here's the kicker"
- Hype: "game-changer", "pushing the boundaries", "paving the way"
- Conclusions: "in conclusion", "to wrap up", "at the end of the day"
- Bot closers: "I hope this helps!", "feel free to reach out"

**Structure check**: Eliminate banned patterns:
- The "It's not X, it's Y" negation pattern (the single most prominent AI tell)
- Self-posed questions answered immediately ("The best part? It's this.")
- Anaphora abuse (same opener 3+ times in a row)
- Present participle trailing clauses ("highlighting its importance", "reflecting broader trends")
- False ranges ("From innovation to implementation")
- Hedge-stacking (multiple qualifiers in one sentence)
- Consecutive adverbial sentence starters

**Punctuation check**:
- Remove em dashes. Replace with commas, periods, parentheses, or colons.
- Remove semicolons (unless user explicitly uses them)
- Remove Oxford commas (unless user explicitly uses them)
- Replace Unicode ellipsis with three dots or restructure

**Rhythm check**:
- Verify sentence length varies (mix 5-word punches with 25-word flows)
- Verify paragraph length varies (some 1-sentence, some 5-sentence)
- Break any Rule of Three that appears back-to-back
- Check for uniform subsection length and vary it

**Formatting check**:
- No bold-first bullet points (every bullet starting with "**Word**: explanation")
- No excessive headers for content that doesn't need them
- No erratic bolding of random words
- No emoji decoration in professional contexts

**Tone check**:
- No relentless positivity. Include criticism where warranted.
- No false balance. Make bold claims when the evidence supports them.
- No emotional flatness. Let genuine reactions show.
- No elevated register for simple ideas.

**Self-reference check**:
- No mentions of being an AI or language model
- No "as someone who..."
- No disclaimers about AI limitations
- No "as of my last knowledge update"
- No "Certainly, here are..."
- Use contractions naturally unless context is genuinely formal

### 5. Verify Authenticity Markers

Ensure output includes profile's authenticity characteristics:
- Acknowledges uncertainty (if specified)
- Shows tradeoffs (if specified)
- Uses specific numbers (if specified)
- References constraints (if specified)

### 6. Final Read-Aloud Test

Read the output in your head. If any sentence sounds like it could appear in any other AI-generated text, rewrite it until it sounds like a specific person said it.

## Usage Examples

### Apply Named Voice

```
User: "Write release notes in technical-authority voice"

Process:
1. Load technical-authority.yaml
2. Generate release notes with:
   - Precise technical terminology
   - Specific version numbers
   - Direct, confident statements
   - Tradeoff acknowledgments where relevant
3. AI tells elimination pass
4. Final read-aloud test
```

### Transform Existing Content

```
User: "Make this documentation more friendly for beginners"

Input: "The API endpoint accepts a JSON payload containing the requisite parameters..."

Process:
1. Load friendly-explainer.yaml
2. Analyze: formal, technical, passive
3. Transform to: casual, accessible, active
4. AI tells elimination pass

Output: "To use this endpoint, send it some JSON with the info it needs..."
```

### Calibrate Voice

```
User: "This is too formal, dial it back 30%"

Process:
1. Identify current formality (~0.8)
2. Calculate target (0.8 - 0.3 = 0.5)
3. Adjust vocabulary and structure for medium formality
4. AI tells elimination pass
```

## Voice Blending

Combine multiple profiles:

```
User: "Write this with 70% technical-authority and 30% friendly-explainer"

Process:
1. Load both profiles
2. Weighted merge:
   - tone.formality: 0.7 * 0.7 + 0.3 * 0.3 = 0.58
   - tone.warmth: 0.7 * 0.3 + 0.3 * 0.8 = 0.45
   - etc.
3. Apply merged profile
4. AI tells elimination pass (always runs last)
```

## Output Format

When reporting voice application:

```
Voice Applied: technical-authority

Transformations:
- Formality: 0.4 -> 0.7 (increased)
- Confidence: 0.5 -> 0.9 (increased)
- Vocabulary: 12 replacements
- Structure: Added 2 examples, removed 1 rhetorical question

AI Tells Check:
- Banned vocabulary removed: 3 instances
- Em dashes replaced: 2 instances
- Banned structures fixed: 1 negation pattern
- Sentence length variance: OK (std dev 7.4)
- Paragraph length variance: OK (varied)

Authenticity Check:
- Acknowledges tradeoffs
- Uses specific numbers
- References constraints
```

## References

- AI Writing Tells (MANDATORY): `references/ai-tells.md`
