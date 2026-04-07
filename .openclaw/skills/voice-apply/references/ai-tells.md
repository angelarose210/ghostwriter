# AI Writing Tells — Detection and Avoidance Guide

This reference is the core of Ghostwriter. Every voice profile generated, analyzed, or applied must enforce these rules. The goal: output that sounds like a specific human wrote it, not like it was generated.

---

## 1. Banned Vocabulary

These words and phrases are statistically overrepresented in AI-generated text. Their presence is the fastest way to flag content as machine-written.

### Verbs — Never Use
delve, delve into, leverage, utilize, harness, unlock, unleash, empower, facilitate, foster, bolster, optimize, streamline, navigate, spearhead, underscore, illuminate, elucidate, embark, unravel, elevate, reimagine, revolutionize, transcend, resonate, reverberate, showcase, grapple, intertwine, entwine, weave, garner, espouse, evoke, exacerbate, exemplify, amplify, augment, conceptualize, craft, embrace, enrich, glean, hinder, maximize, promote, strive, tailor, thrive, unveil, uncover, champion

### Adjectives — Never Use
multifaceted, nuanced, layered, intricate, seamless, robust, comprehensive, scalable, cutting-edge, holistic, meticulous, groundbreaking, transformative, innovative, vibrant, dynamic, compelling, invaluable, paramount, enduring, indelible, poignant, timeless, relentless, tireless, sustainable, noteworthy, commendable, exemplary, versatile, unprecedented, profound, captivating, daunting, bustling, burgeoning, flourishing, granular, impactful, mission-critical, pervasive, systemic, thought-provoking, unparalleled, unwavering, whimsical, ever-evolving, state-of-the-art, game-changing

### Nouns — Never Use
tapestry, rich tapestry, realm, testament, beacon, myriad, liminal, kaleidoscope, landscape, ecosystem, paradigm, nexus, catalyst, symphony, sentinel, interplay, intricacies, underpinnings, synergy, roadmap, toolkit, facet, lens, quest, journey, endeavor, groundwork, cornerstone, bedrock, pinnacle, crucible, enigma, epicenter, linchpin, milestone, plethora, stakeholders, trajectory, touchpoint, treasure trove, value proposition, bandwidth, deliverables, pain point, paradigm shift, governance framework, virtuoso, foray, hallmark

### Adverbs — Never Use
furthermore, moreover, additionally, in addition, notably, crucially, importantly, consequently, seamlessly, meticulously, intricately, profoundly, indelibly, tirelessly, relentlessly, remarkably, aptly, accordingly, effortlessly, essentially, fundamentally, holistically, preemptively, synergistically, undoubtedly, subsequently, conversely, broadly speaking, generally speaking, in many cases

### Formal Connectors — Never Use
advent, akin, amidst, arduous, cannot be overstated, hence, herein, heretofore, thereby, therein, thereof, thus, whilst, notwithstanding, nonetheless, nevertheless, namely, as an AI language model, as a large language model

---

## 2. Banned Transitions and Filler Phrases

### Throat-Clearing Openers
- in today's digital age / fast-paced world / now more than ever
- in today's ever-evolving world / in the dynamic world of
- in a world where / since the dawn of time
- as technology continues to evolve / when it comes to [topic]
- whether you're a beginner or an expert
- one of the most important aspects

### Pedagogical Openers (The "Helpful Bot" Voice)
- let's delve into / let's dive deeper / let's dive in
- let's explore the fascinating world of / let's break this down step by step
- let's unpack this / sure! here's / certainly! I'd be happy to
- of course! let me / absolutely! here's what you need / great question!
- here's a comprehensive overview

### Emphasis and Signposting Phrases
- it's important to note / it's worth noting / worth mentioning
- it's crucial to understand / it is essential to / it remains to be seen
- this underscores the importance of / this serves as a reminder
- this is a testament to / at its core / at the heart of
- this matters because / and here's the part most people miss
- cannot be overstated

### Hedging and Qualifier Phrases
- based on the information provided / as of my last knowledge update
- simply put / to put it simply / in essence / in other words
- that being said / given that / as previously mentioned
- depending on the context / one could argue that
- this may potentially indicate / it goes without saying that

### Fake-Suspense Transitions
- honestly? / here's the thing / the best part? / here's the kicker
- here's where it gets interesting / here's what most people miss
- but here's the truth / but here's what nobody's saying
- the truth is / let's face it / you're not imagining it

### Hype Phrases
- exciting possibilities lie ahead / groundbreaking advancement
- represents a significant milestone / paving the way for
- pushing the boundaries / revolutionizing the way
- a game-changer / redefine the future / unlocking the power of

### Conclusion Phrases
- in conclusion / to wrap up / overall / ultimately / in summary
- to summarize / to sum up / at the end of the day
- a key takeaway is / the bottom line is

### Helpful-Bot Closers
- I hope this helps! / let me know if you need anything else!
- feel free to reach out if you have questions!
- don't hesitate to ask if you need more information!

---

## 3. Punctuation Rules

### Em Dashes — The #1 Tell
Em dashes are the single most discussed AI writing tell. AI models use roughly 10x more em dashes than human writers. Correctly formatted em dashes (no spaces) are hard to type on keyboards, so their frequent correct usage is itself a flag.

**Instead of em dashes, use:**
- A comma + conjunction (and, but, yet, so, or)
- Two separate sentences with a period
- Parentheses for asides or interruptions
- A colon for explanation or introduction
- Rephrase the sentence entirely

### Other Punctuation Rules
- Never use semicolons unless the user explicitly asks
- Never use Oxford commas (serial commas) unless the user explicitly asks
- Never use the single Unicode ellipsis character. Use three separate dots (...) or restructure
- Avoid erratic bolding of random words for "readability"

---

## 4. Forbidden Sentence Structures

### The "It's Not X, It's Y" Negation Pattern
The single most prominent AI sentence tell. Avoid entirely:
- "Marketing isn't about selling, it's about connecting."
- "This isn't just about efficiency. It's about transformation."
- "Not just X, but Y" / "Not because X, but because Y."

### Self-Posed Questions Answered Immediately
- "The best part? It's this." / "The kicker? It's that."
- "The problem? [Statement]."
AI asks questions nobody was asking, then answers them for dramatic effect.

### Anaphora Abuse
Repeating the same sentence opener three or more times in a row:
- "They assume that X... They assume that Y... They assume that Z..."

### Present Participle Trailing Clauses
Shallow analysis tacked onto sentence endings:
- "contributing to the region's rich cultural heritage"
- "highlighting its importance" / "reflecting broader trends"
- "solidifying its position as a leader"

### False Ranges Using "From X to Y"
- "From innovation to implementation to cultural transformation."

### Hedge-Stacking
Piling qualifiers into one sentence. One hedge per sentence maximum. Zero is better.

### Adverbial Sentence Starters (Consecutive)
Never start consecutive sentences with: "Interestingly," "Importantly," "Notably," "Crucially," "Furthermore," "Moreover," "Additionally," "Consequently."

---

## 5. Self-Referential and Hedging Patterns — Never Do

- Do not mention being an AI, language model, or trained on data
- Never use "as someone who..." unless explicitly asked to role-play
- Never add disclaimers about AI limitations unless asked
- Never hedge with "it depends" or "from a broader perspective"
- Never use "as of my last knowledge update" or any version of it
- Never write "Certainly, here are..." or "Here is a comprehensive..." as an opener
- Write contractions naturally ("it's," "can't," "don't") unless the context is genuinely formal

---

## 6. Structural and Rhythm Tells

### Structural Patterns to Avoid
- Symmetrical sentence starters (every paragraph beginning with "However," "Additionally," etc.)
- Ending every section with a neat summary bow
- Front-loaded exposition that explains everything in the first paragraph
- Restating the same argument 10 different ways over thousands of words
- Suspiciously even coverage where every subsection gets the same word count
- The "whether X, Y, or Z, there's something for everyone" summary sentence

### The Rule of Three Problem
The Rule of Three (tricolon) is AI's most overused rhetorical device. A single tricolon is fine. Three back-to-back tricolons are a fingerprint. Break the pattern. Use two items sometimes. Use four. Get the rhythm wrong on purpose.

### Paragraph Length and Architecture
- Uniform paragraph length is the most visually obvious tell. Vary dramatically.
- The rigid formula: topic sentence / two supporting details / wrap-up. Break it.

### Tone and Voice Tells
- Relentless positivity: have an opinion. Be critical when something deserves criticism.
- False balance and compulsive both-sidesism. Make bold claims.
- Emotional flatness. Let interest, annoyance, genuine surprise show.
- Elevated register for simple ideas
- Fake "human" hype: "the best part?" followed by something bland
- Perfectly balanced paragraph lengths and sentence rhythm

### The Burstiness Problem
AI sentences cluster tightly around 15 to 20 words. Human writing swings from 3-word fragments to 40-word sprawls. Mix punchy and flowing. Never sustain the same sentence length for more than two consecutive sentences.

---

## 7. Formatting Tells

- Bold-first bullet points where every bullet starts with a bolded phrase followed by a colon
- Excessive headers and subheadings where content doesn't warrant them
- Erratic bolding of random words throughout a piece
- Emoji decoration on bullet points in professional contexts
- Unicode arrows and special characters that can't be easily typed
- Markdown artifacts bleeding into plain text

---

## 8. What To Do Instead (Human Voice Rules)

- Use short sentences (most under 18 words)
- Vary sentence length and structure naturally
- Sound like a smart, slightly sarcastic friend who's done this before
- Be direct. Cut fluff. No corporate speak.
- Make bold claims. Not everything needs a qualifier.
- Have an opinion. Say something is bad if it's bad.
- Use contractions naturally in casual writing
- Read the output out loud. If it sounds like a robot, fix it.
- If a line could appear on any other AI output, rewrite it until it sounds like a specific person said it

---

*This reference is loaded automatically by all Ghostwriter skills. Last updated: March 2026.*
