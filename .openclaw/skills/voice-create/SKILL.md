---
name: voice-create
description: "Generate custom voice profiles from natural language descriptions. Use when user wants to create a new writing voice from a description rather than from samples."
version: 1.0.0
platforms: [all]
metadata: { "openclaw": { "requires": {} } }

---

# voice-create

Generate custom voice profiles from natural language descriptions. Every generated profile includes AI tells avoidance rules by default.

## Triggers

Alternate expressions and non-obvious activations (primary phrases are matched automatically from the skill description):

- "make me sound like [reference]" -> reference-based voice creation
- "voice fingerprint" -> voice profile extraction from text

## Behavior

When triggered, this skill:

1. **Parses the description** to identify:
   - Target audience (developers, executives, general public)
   - Tone characteristics (formal/casual, confident/tentative, warm/clinical)
   - Domain context (technical, marketing, academic, conversational)
   - Any specific constraints or preferences mentioned

2. **Maps description to voice dimensions**:
   - Formality (0-1): casual <-> formal
   - Confidence (0-1): hedging <-> assertive
   - Warmth (0-1): clinical <-> friendly
   - Energy (0-1): calm <-> enthusiastic
   - Complexity (0-1): simple <-> sophisticated

3. **Generates vocabulary guidance**:
   - Preferred terms based on domain
   - Terms to avoid based on tone
   - Signature phrases that match the voice
   - **Always includes AI tells avoidance**: every generated profile's `vocabulary.avoid` list includes the full set of banned AI vocabulary from `../voice-apply/references/ai-tells.md`

4. **Creates structure patterns**:
   - Sentence length preferences
   - Paragraph structure
   - Use of lists, examples, analogies
   - **Always enforces human-like rhythm**: high sentence length variance, varied paragraph lengths, em dash avoidance, no Rule of Three abuse

5. **Adds anti-AI-tells rules**:
   - `punctuation.em_dashes`: avoid (default for all generated profiles)
   - `punctuation.semicolons`: avoid (unless user specifies formal/academic)
   - `structure.sentence_length_variance`: high (enforces burstiness)
   - `structure.paragraph_length_variance`: high (prevents uniform blocks)
   - `structure.rule_of_three`: break-pattern (vary item counts)
   - `banned_patterns`: negation flips, self-posed questions, anaphora, trailing participles, hedge-stacking

6. **Outputs valid YAML** conforming to voice-profile schema

## Usage Examples

### Technical Documentation Voice
```
User: "Create a voice for API documentation - precise, no-nonsense, assumes developer knowledge"

Output: technical-api-docs.yaml
- formality: 0.6
- confidence: 0.9
- warmth: 0.2
- energy: 0.3
- complexity: 0.8
- vocabulary.prefer: technical terms, code references, precise metrics
- vocabulary.avoid: [all AI tells] + marketing language
- structure: varied sentence length, no em dashes
```

### Friendly Tutorial Voice
```
User: "Make me a voice for beginner tutorials - encouraging, patient, uses lots of analogies"

Output: beginner-tutorial.yaml
- formality: 0.2
- confidence: 0.7
- warmth: 0.9
- energy: 0.7
- complexity: 0.3
- vocabulary.prefer: everyday language, encouraging phrases, analogies
- vocabulary.avoid: [all AI tells] + jargon
- structure: short sentences mixed with longer explanations, no "let's dive in" openers
```

### Executive Summary Voice
```
User: "Generate a voice profile for board presentations - authoritative but accessible"

Output: board-presentation.yaml
- formality: 0.8
- confidence: 0.9
- warmth: 0.4
- energy: 0.5
- complexity: 0.6
- vocabulary.prefer: business metrics, strategic language, clear conclusions
- vocabulary.avoid: [all AI tells] + buzzwords like "synergy", "paradigm", "stakeholders"
- structure: varied paragraph lengths, direct openers, no "in conclusion" closers
```

## Output Location

Generated profiles are saved to:
1. `.aiwg/voices/{name}.yaml` (project-specific, default)
2. `~/.config/aiwg/voices/{name}.yaml` (user-wide, with --global flag)

## Voice Generation Process

### Step 1: Dimension Calibration

Parse natural language for dimension indicators:

| Description Keywords | Dimension | Value Range |
|---------------------|-----------|-------------|
| casual, relaxed, conversational | formality | 0.1-0.3 |
| professional, business | formality | 0.5-0.7 |
| formal, academic, official | formality | 0.8-1.0 |
| tentative, careful, hedging | confidence | 0.2-0.4 |
| balanced, measured | confidence | 0.5-0.7 |
| assertive, authoritative, direct | confidence | 0.8-1.0 |
| clinical, detached, objective | warmth | 0.1-0.3 |
| neutral, professional | warmth | 0.4-0.6 |
| friendly, warm, personable | warmth | 0.7-0.9 |
| calm, measured, understated | energy | 0.1-0.3 |
| balanced, engaged | energy | 0.4-0.6 |
| enthusiastic, dynamic, energetic | energy | 0.7-0.9 |
| simple, accessible, plain | complexity | 0.1-0.3 |
| clear, moderate | complexity | 0.4-0.6 |
| sophisticated, detailed, nuanced | complexity | 0.7-0.9 |

### Step 2: Domain Detection

Identify domain from context:
- **Technical**: API, code, system, architecture, implementation
- **Marketing**: brand, campaign, audience, engagement, conversion
- **Academic**: research, methodology, analysis, findings, literature
- **Executive**: strategy, ROI, decision, outcome
- **Support**: help, issue, solution, troubleshoot, resolve

### Step 3: Vocabulary Generation

Based on domain and tone, generate:
- 5-10 preferred terms
- 3-5 domain-specific terms to avoid
- 2-4 signature phrases
- **Mandatory**: merge the full AI tells banned vocabulary list into `vocabulary.avoid`. This list includes 50+ banned verbs, 40+ banned adjectives, 40+ banned nouns, 30+ banned adverbs, and all banned connectors. See `../voice-apply/references/ai-tells.md` for the complete lists.

### Step 4: Structure Selection

Map tone to structure patterns:
- High formality -> longer sentences, structured paragraphs
- Low formality -> shorter sentences, varied structure
- High confidence -> direct statements, conclusions first
- High warmth -> questions, inclusive language ("we", "let's")

**Always enforce**:
- `sentence_length_variance: high` (mix 5-word punches with 30-word flows)
- `paragraph_length_variance: high` (mix 1-sentence paragraphs with 5-sentence paragraphs)
- `em_dash_usage: avoid` (use commas, periods, parentheses, colons instead)
- `rule_of_three: break-pattern` (use 2 items or 4 items to break the AI fingerprint)

### Step 5: Anti-Pattern Rules

Every generated profile includes these structure rules:

```yaml
anti_ai_tells:
  # Sentence patterns to never use
  banned_patterns:
    - negation_flip          # "It's not X, it's Y"
    - self_posed_questions   # "The best part? It's this."
    - anaphora_abuse         # Same opener 3+ times
    - trailing_participles   # "highlighting its importance"
    - false_ranges           # "From innovation to implementation"
    - hedge_stacking         # Multiple qualifiers per sentence
    - consecutive_adverbials # Starting sentences with "Furthermore," "Moreover," etc.
  # Punctuation rules
  punctuation:
    em_dashes: avoid
    semicolons: avoid
    oxford_commas: avoid
    unicode_ellipsis: never
  # Formatting rules
  formatting:
    bold_first_bullets: never
    excessive_headers: avoid
    erratic_bolding: never
    emoji_in_professional: never
  # Rhythm rules
  rhythm:
    sentence_length_variance: high    # std dev > 6 words
    paragraph_length_variance: high   # mix short and long
    uniform_subsections: never        # vary section lengths
  # Tone rules
  tone_guards:
    relentless_positivity: avoid      # be critical when warranted
    false_balance: avoid              # make bold claims
    emotional_flatness: avoid         # show genuine reactions
    elevated_register_for_simple: avoid  # match register to content
```

## Integration

Works with other voice-framework skills:
- Created voices can be applied via `voice-apply`
- Created voices can be inputs to `voice-blend`
- `voice-analyze` can create base profiles that `voice-create` refines
- All created voices automatically include AI tells avoidance

## References

- AI Writing Tells: `../voice-apply/references/ai-tells.md`
