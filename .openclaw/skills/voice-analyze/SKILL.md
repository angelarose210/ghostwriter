---
name: voice-analyze
description: "Reverse-engineer voice profiles from sample content by analyzing writing patterns. Use when user pastes writing samples and wants to extract their style."
version: 1.0.0
platforms: [all]
metadata: { "openclaw": { "requires": {} } }

---

# voice-analyze

Reverse-engineer voice profiles from sample content by analyzing writing patterns. Detects and flags AI writing tells so the resulting profile produces human-sounding output.

## Triggers

Alternate expressions and non-obvious activations (primary phrases are matched automatically from the skill description):

- "voice fingerprint" -> voice profile extraction
- "what's my writing style" -> voice analysis

## Behavior

When triggered, this skill:

1. **Analyzes text samples** for:
   - Sentence structure and length patterns
   - Vocabulary sophistication and domain
   - Tone markers (formality, confidence, warmth)
   - Structural patterns (lists, examples, questions)
   - Perspective and voice choices

2. **Extracts measurable features**:
   - Average sentence length
   - Vocabulary complexity (syllables, word length)
   - Contraction usage
   - Personal pronoun frequency
   - Question density
   - List/bullet usage

3. **Scans for AI writing tells** (see `../voice-apply/references/ai-tells.md`):
   - Flags any banned vocabulary found in the sample (verbs, adjectives, nouns, adverbs from the tells list)
   - Detects banned sentence structures: "It's not X, it's Y" negation patterns, self-posed questions answered immediately, anaphora abuse, present participle trailing clauses
   - Measures em dash frequency (AI models use ~10x more than human writers)
   - Checks for uniform sentence length clustering (the "burstiness problem": AI clusters at 15-20 words, humans swing from 3-word fragments to 40-word sprawls)
   - Detects banned transitions and filler phrases (throat-clearing openers, pedagogical openers, fake-suspense transitions, hype phrases)
   - Flags formatting tells: bold-first bullet points, excessive headers, erratic bolding, emoji decoration
   - Checks for Rule of Three overuse (back-to-back tricolons are an AI fingerprint)
   - Detects uniform paragraph length (the most visually obvious tell)
   - If the sample contains AI tells, the profile's `vocabulary.avoid` list MUST include them and the `ai_tells_report` section must document what was found

4. **Maps features to voice dimensions**:
   - Statistical analysis -> tone scale values (0-1)
   - Pattern detection -> structure preferences
   - Vocabulary extraction -> prefer/avoid lists

5. **Generates voice profile** matching the analyzed style, with AI tells filtered out

## Usage Examples

### Analyze Existing Documentation
```
User: "Analyze this writing style" + [paste technical docs]

Analysis:
- Formality: 0.7 (no contractions, structured sentences)
- Confidence: 0.85 (direct statements, few hedges)
- Warmth: 0.25 (impersonal, third-person)
- Complexity: 0.8 (technical vocabulary, long sentences)
- AI Tells Detected: 3 (2 banned verbs, 1 negation pattern)

Output: analyzed-technical-docs.yaml
```

### Match Brand Voice
```
User: "Extract voice from our marketing copy" + [paste samples]

Analysis:
- Formality: 0.3 (conversational, contractions)
- Confidence: 0.7 (benefit claims, but some hedging)
- Warmth: 0.85 (second person, friendly tone)
- Energy: 0.8 (exclamation points, action verbs)
- AI Tells Detected: 0

Output: brand-marketing-voice.yaml
```

### Capture Personal Style
```
User: "Create profile from my blog posts" + [paste samples]

Analysis:
- Identifies personal writing quirks
- Extracts signature phrases
- Maps to voice dimensions
- Flags and excludes any AI tells found in samples

Output: personal-blog-voice.yaml
```

## Analysis Methodology

### Feature Extraction

| Feature | Measurement | Maps To |
|---------|-------------|---------|
| Sentence length | Avg words/sentence | complexity |
| Sentence length variance | Std deviation of word count | burstiness (human = high variance) |
| Contractions | Frequency per 100 words | formality (inverse) |
| First person ("I", "we") | Frequency | warmth |
| Second person ("you") | Frequency | warmth |
| Passive voice | Percentage of sentences | confidence (inverse) |
| Questions | Per paragraph | warmth, engagement |
| Hedging words | "might", "perhaps", "could" | confidence (inverse) |
| Exclamation marks | Frequency | energy |
| Technical terms | Domain vocabulary density | complexity |
| Em dash frequency | Per 1000 words | ai_tell_score (high = likely AI) |
| Banned AI vocabulary | Count from tells list | ai_tell_score |
| Paragraph length variance | Std deviation of sentence count | ai_tell_score (low variance = likely AI) |

### AI Tells Detection Pass

After standard feature extraction, run the AI tells scan. For each category in `../voice-apply/references/ai-tells.md`:

1. **Vocabulary scan**: Count occurrences of every word/phrase in the banned lists (verbs, adjectives, nouns, adverbs, connectors)
2. **Structure scan**: Detect banned sentence patterns (negation flips, self-posed questions, anaphora, trailing participles, false ranges, hedge-stacking)
3. **Punctuation scan**: Count em dashes, semicolons, Oxford commas, Unicode ellipsis characters
4. **Rhythm scan**: Calculate sentence length standard deviation. If std dev < 4 words, flag as AI-like clustering
5. **Formatting scan**: Check for bold-first bullets, excessive headers, erratic bolding
6. **Transition scan**: Search for throat-clearing openers, pedagogical openers, fake-suspense phrases, hype phrases, banned conclusion phrases

Report findings in the output profile under `ai_tells_report`. Any banned vocabulary found in the sample goes into `vocabulary.avoid` automatically.

### Dimension Calibration

**Formality** (0-1):
- 0.0-0.3: Contractions frequent, casual language, fragments okay
- 0.4-0.6: Mixed style, professional but accessible
- 0.7-1.0: No contractions, complete sentences, formal structure

**Confidence** (0-1):
- 0.0-0.3: Many hedges ("might", "perhaps"), questions, qualifiers
- 0.4-0.6: Balanced certainty, occasional hedges
- 0.7-1.0: Direct statements, conclusions first, few qualifiers

**Warmth** (0-1):
- 0.0-0.3: Third person, passive voice, clinical tone
- 0.4-0.6: Professional but personable
- 0.7-1.0: Second person, inclusive language, empathetic

**Energy** (0-1):
- 0.0-0.3: Calm, measured, understated
- 0.4-0.6: Balanced engagement
- 0.7-1.0: Exclamation marks, action verbs, dynamic phrasing

**Complexity** (0-1):
- 0.0-0.3: Short sentences, simple vocabulary, accessible
- 0.4-0.6: Moderate complexity, clear but nuanced
- 0.7-1.0: Long sentences, technical vocabulary, layered ideas

### Vocabulary Extraction

**Signature phrases** - Identified by:
- Repeated patterns across samples
- Distinctive constructions
- Opening/closing patterns

**Domain vocabulary** - Extracted by:
- Technical term frequency
- Specialized jargon
- Industry-specific language

**Avoid patterns** - Built from two sources:
1. Conspicuous absence of common phrases in the samples
2. Any AI writing tells found during the tells detection pass (always include these)

## Output Format

```yaml
name: analyzed-sample-voice
version: 1.0.0
description: Voice profile extracted from sample content
analysis_source:
  sample_size: 1500  # words analyzed
  sample_count: 3    # number of samples
  confidence: 0.85   # analysis confidence score
tone:
  formality: 0.65
  confidence: 0.8
  warmth: 0.4
  energy: 0.5
  complexity: 0.7
vocabulary:
  prefer:
    - "extracted signature phrase 1"
    - "detected domain terminology"
  avoid:
    - "leverage"       # AI tell: banned verb
    - "delve"          # AI tell: banned verb
    - "comprehensive"  # AI tell: banned adjective
    - "landscape"      # AI tell: banned noun
    - "furthermore"    # AI tell: banned adverb
    - "patterns not found in samples"
  signature_phrases:
    - "The key point is..."
    - "This demonstrates..."
structure:
  sentence_length: medium    # avg 15-20 words
  sentence_length_variance: high  # std dev > 6 words (human-like)
  paragraph_length: medium   # avg 4-6 sentences
  paragraph_length_variance: high # varied paragraph sizes (human-like)
  sentence_variety: high     # varied structure detected
  use_lists: when-appropriate
  use_examples: frequently
  use_questions: rarely
  em_dash_usage: avoid       # always set to avoid unless user explicitly uses them naturally
perspective:
  person: third
  voice: active
  tense: present
extracted_patterns:
  opening_style: "context-first"
  closing_style: "conclusion-summary"
  transition_style: "logical-flow"
ai_tells_report:
  tells_found: 3
  em_dash_frequency: 2.1     # per 1000 words (human avg ~0.5, AI avg ~5.0)
  sentence_length_std_dev: 7.2  # words (human = 6-12, AI = 2-4)
  paragraph_length_std_dev: 2.8 # sentences (human = 2-5, AI = 0.5-1.5)
  banned_vocabulary_found:
    - "leverage (1x)"
    - "comprehensive (2x)"
  banned_structures_found:
    - "negation pattern (1x)"
  banned_transitions_found: []
  formatting_tells_found: []
  overall_human_score: 0.82  # 0 = clearly AI, 1 = clearly human
```

## Integration

- **Output**: Creates profiles usable by `voice-apply`
- **Chain**: `voice-analyze` -> `voice-create` (to refine) -> `voice-apply`
- **Chain**: `voice-analyze` + `voice-analyze` -> `voice-blend` (combine styles)

## Accuracy Considerations

- **Minimum sample**: 500+ words for reliable analysis
- **Multiple samples**: 3+ samples improve accuracy
- **Consistent genre**: Mixing genres reduces accuracy
- **Confidence score**: Output includes analysis confidence (0-1)
- **AI tells in samples**: If the sample itself contains AI tells (e.g., it was partially AI-generated), the analyzer will flag them and exclude them from the profile's preferred patterns. The `overall_human_score` helps gauge how much of the sample is genuinely the user's voice vs AI artifacts.

## References

- AI Writing Tells: `../voice-apply/references/ai-tells.md`
