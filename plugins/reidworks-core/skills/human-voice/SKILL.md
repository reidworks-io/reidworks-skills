---
name: human-voice
description: Edit or write external-facing prose so it doesn't read as AI-generated. Apply to documentation, blog posts, tutorials, public READMEs, customer-facing slide decks, marketing copy, and competitive briefs — whenever the user asks to write, edit, review, or style-check such content, even if they don't mention AI. Apply when creating this kind of content from scratch. Do NOT apply to internal communications (Slack, Notion, internal PRs, meeting notes) unless the user explicitly asks for a style review. Trigger phrases include "write a blog post", "edit this doc", "review this tutorial", "write copy for", "external-facing", "customer-facing", "public README", "slide deck for customers", "competitive brief", "does this sound AI-generated", "check this for AI tells", "make this less AI", "remove the slop".
metadata:
  category: writing
  author: mscwilson
---

# Human Voice

AI-generated content has recognisable patterns that undermine credibility with technical readers. This skill defines constraints to prevent them.

## Core principle

Write like a person explaining something to a colleague. Not like a documentary narrator, not like a marketing brochure. If a sentence would sound strange said aloud to a coworker, rewrite it.

## Content-type strictness

- **Documentation and tutorials**: Strictest. No marketing language. No drama. Precision over everything.
- **Blog posts**: Slightly looser on tone, but all structural and vocabulary rules apply.
- **Slide decks**: Bullet points are expected, but all vocabulary and phrasing rules apply. Slides have additional AI tells — see section 8.
- **Sales and competitive content**: All rules apply regardless of format. Sales content has its own failure modes — see section 8.

---

## Rules

### 1. Prohibited vocabulary

Do not use these words and phrases. They are AI tells.

**Single words:** crucial, pivotal, vital, comprehensive, robust, seamless, streamline, leverage (as a verb), foster, garner, underscore, showcase, delve, vibrant, tapestry, landscape (figurative), empower, unlock, harness, elevate, nuanced, intricate, multifaceted, actionable, holistic, paradigm, synergy, genuinely, intriguing, brilliant, aggressive/aggressively (as intensifier), non-starter, non-negotiable, game-changer

**Phrases:**

- "It's important/crucial/worth noting that..." — state the thing directly
- "This is a testament to..."
- "In today's [anything]..." / "In the ever-evolving..."
- "Serves as / stands as / marks a" — use "is"
- "At its core..."
- "Whether you're a... or a..." — the false-inclusive address; reframe the whole opening
- "Not just X, but Y" — rhetorical escalation
- "End to end" / "at scale" — unless technically precise
- "A few things worth noting:" — write sentences instead
- "Here's what that looks like:" — just show it
- "Let's dive in" / "Let's explore" / "Let's take a closer look"
- "a much richer [noun]" / "a richer analytical surface" — AI compound nouns
- "a constant game of [gerund]" / "a balancing act between" — forced-casual constructions
- "without any additional [noun] work" — overstates what's been eliminated; say specifically what isn't needed
- "Garbage in, garbage out" — stock phrase standing in for a specific argument about data quality
- "at every layer" / "across the board" — vague scope claims; name the layers or drop the phrase
- "the question is [X] vs [Y]" — false binary framing dressed as clarity; state your actual point

**AI-preferred technical verbs:** Do not use wire, scaffold, spin up, hydrate, surface, enrich (unless it's a precise technical term in your domain), or encode to mean "write down/document." Use the plain verb: connect, add, start, populate, show, document.

### 2. Em dash rules

Em dashes are one of the strongest AI tells in prose. Even when each individual use is defensible, density gives the game away.

**Limits by content type:**

- Documentation, tutorials, and slide decks: zero em dashes. Rewrite every instance.
- Blog posts and long-form prose: maximum one em dash per piece.

**Rewriting parentheticals.** The most common "defensible" use is a parenthetical aside. Use one of these instead:

- Commas: "AI crawlers, the ones feeding LLM training pipelines, are less orderly."
- Two sentences: "AI crawlers are less orderly. These are the ones feeding LLM training pipelines and retrieval systems."

**Rewriting other common uses:**

- Dramatic asides ("The browser sends the message — but that's all it knows"): two sentences.
- Rhetorical escalation ("Not just a purchase — a purchase from a premium customer"): drop the escalation, state the point once.
- Promotional tails (benefit clauses tacked onto a sentence): separate sentence stating specifically what isn't needed.
- Lists mid-sentence with summary tail ("crawlers, uptime monitors, link checkers — the usual background noise"): end at the last list item and start a new sentence, or drop the summary phrase entirely.

### 3. No cinematic writing

**Scene-setting fragments:** Do not open examples with screenplay-style fragments. "Consider a travel booking chatbot. A user types a query. Behind the scenes:" — rewrite as a normal explanatory sentence.

**Three-beat punchlines:** Do not use sequences of three short escalating sentences for effect. "Same model. Same question. Dramatically better response." — rewrite as one normal sentence.

**Theatrical transitions:** Do not use "Now for the main event —" / "Enter the new API." / "This is where it gets interesting." The content should speak for itself.

**Foreshadowing:** Do not write "More on that in a later section." Link to the section or don't mention it.

**Self-referential callbacks:** Do not write "This is why the earlier tip matters:" or "As we mentioned above:" — if the point is worth repeating, restate it directly without meta-commentary.

**End-of-page trailers:** Do not add summary-plus-preview paragraphs at the end of sections or pages. End when the content ends. At most, one short transitional sentence.

**Performed deliberation:** Do not state a position and then immediately contradict it as a rhetorical device to simulate balanced thinking. State the tradeoff once.

### 4. No overstatement

**False contrasts:** Do not imply the alternative approach is uninteresting or inadequate unless you can state specifically why.

**Unsubstantiated comparatives:** Do not write "smarter," "richer," "deeper," or "better" without naming the baseline. "Richer data" and "richer features" are especially common AI reaches — say what the data contains that makes it more useful, don't just call it rich. If you can't name the baseline, drop the comparative or say what makes it different.

**Marketing adjectives:** Do not write "meaningful," "powerful," "elegant," or "sophisticated" unless the meaning is precise and necessary. If you can't say what makes it meaningful, drop the word.

**Grandiose scope claims:** Do not write "complete transparency" or "from zero to full observability" unless those terms have a specific technical referent defined earlier in the content.

**Dramatised escalation:** Do not use the "what started as X becomes Y" structure. State the cost or outcome directly.

**Speculation as fact:** If you're inferring from limited evidence, say so. Use "this suggests" or "could create" rather than asserting.

**Fake-precise numbers:** Do not invent specific multipliers or ranges to sound concrete ("4–5× increase," "2× the coverage," "10+ years"). If you have a real number from a real source, cite it. If you don't, make the argument without a number.

**Arrow chains as causal reasoning:** Do not use "X → Y → Z" as inline shorthand for an argument. This skips the actual reasoning. Either make the causal claim in a sentence or put the chain in a diagram where the visual format earns it.

### 5. Structural AI tells

**No two-item lists.** If you have two points, write two sentences.

**No bold first sentences as pseudo-headings.** A bold fragment followed by a full stop and then explanatory prose is a fake heading — use a real heading or restructure. Bold terms or phrases used inline within a sentence are fine.

**No formulaic headings.** Do not use: "Putting It All Together," "The Full Flow," "Getting Started," "Conclusion and Next Steps," "What You'll Need," "What's Next." Use headings that describe the actual content.

**No rhetorical question headings.** "What Even Is a Skill?" / "What's the Bar?" — name the content instead.

**Parenthetical context should be prose.** If a parenthetical is doing real explanatory work, give it a full sentence.

**No unnecessary numbering.** Do not format every sequential process as Step 1 / Step 2 / Step 3 if the steps aren't truly discrete or ordered. Do not number rhetorical beats that aren't steps.

**Summaries should not restate the introduction.** A summary states conclusions or next steps. Don't re-explain products or concepts in the conclusion.

### 6. Tense and address

**Use future tense for instructions the reader hasn't done yet.** "You'll create" not "you create" for steps that are ahead of the reader.

**Do not flatter the reader.** "As a business expert, you already know..." — just state the fact.

**Do not anthropomorphise technical components.** Browsers don't "know" things. Say what they have access to.

### 7. Formatting

**Use code blocks, not quote blocks, for anything the reader might copy.** Code blocks have copy buttons; quote blocks don't. Use language tag `txt` for plain text. This applies to documentation or tutorials only.

**Use inline code for all identifiers.** Variable names, field names, schema names, config keys — anything that's a literal identifier gets backtick formatting.

### 8. Competitive and sales content

**No consultancy stock phrases.** Do not use: "best-of-breed," "category leader," "market leader," "table stakes," "the composable answer," "the [adjective] era," "future-proof." Name the specific advantage instead.

**No concede-then-diminish.** Do not acknowledge a competitor's strength only to immediately undercut it. If the point is that a capability is limited in scope, say that directly without the rhetorical setup.

**Competitor comparisons should be specific.** Name the specific capability, say what the competitor does, say what you do differently, and say why the difference matters for the customer. If you can't fill in all four parts, the comparison isn't ready.

**Do not repeat the same claim across slides.** State a point once.

**No rigid binary columns as default structure.** Side-by-side comparison columns are legitimate for specific feature comparisons. They are not the default structure for every slide in a deck.

---

## Examples

Concrete before/after examples are in `references/examples.md`. Read that file when you need to see how a specific pattern plays out in practice.
