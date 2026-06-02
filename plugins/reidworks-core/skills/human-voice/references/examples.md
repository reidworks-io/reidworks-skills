
# Before/After Examples

Real examples from Snowplow content, showing AI-generated text and how to fix it. Read this file when you need concrete examples of the rules in SKILL.md.

## Em dash + dramatic aside

**Before:**
> The browser sends the message and eventually renders a response — but that's all it knows.

**After:**
> The browser sends the message and eventually renders a response. It has no visibility into what happens server-side.

**Why:** Em dash introduces an anthropomorphised dramatic aside. The browser doesn't "know" things.

---

## Cinematic scene-setting

**Before:**
> Consider a travel booking chatbot. A user types "find me cheap flights to Paris tomorrow." Behind the scenes:

**After:**
> Take a travel booking chatbot as an example. When a user asks for cheap flights to Paris, several things happen that aren't visible from the browser:

**Why:** The original reads like a screenplay. Fragment sentences create false drama. Technical writing should just explain.

---

## Three-beat punchline

**Before:**
> Same model. Same question. Dramatically better response.

**After:**
> The response is much more useful, even though the model and question are identical.

**Why:** Three short escalating fragments is a copywriting technique. In technical content it reads as AI trying to sound punchy.

---

## Parenthetical context dump

**Before:**
> With Signals context (user has spent 20 minutes on the enterprise pricing page):

**After:**
> Adding real-time context from Signals can improve responses. In this example, the user has spent 20 minutes exploring the enterprise pricing page:

**Why:** The parenthetical is doing real work — it's the setup for the example. Give it a proper sentence.

---

## "Not just X, but Y" with em dash

**Before:**
> Think of them as metadata you send alongside each conversion — not just "a purchase happened," but "a purchase happened, and this customer is in the premium LTV band with a particular interest in these product categories."

**After:**
> They're metadata you send alongside each conversion. Instead of just recording "a purchase happened," you can record which LTV band the customer falls into and which product categories they've been browsing.

**Why:** The "not just X, but Y" structure is a classic AI rhetorical escalation, here combined with an em dash. The rewrite says the same thing without the rhetorical device.

---

## Theatrical transition

**Before:**
> Now for the main event — connecting Signals to your AI agent via the Vercel AI SDK.

**After:**
> The next step is to connect Signals to your AI agent, via the Vercel AI SDK.

**Why:** "Now for the main event" is AI theatrics. Technical writing doesn't need to build excitement.

---

## Theatrical transition with AI technical verb

**Before:**
> In this post, we'll walk through how to wire the two together. No custom infrastructure required — just user attributes, targeting rules, and a few lines of SDK code.

**After:**
> This post explains how to connect Signals and Statsig. You'll pass user attributes, set up targeting rules, and add a few lines of SDK code.

**Why:** "Walk through" + "wire together" are both AI-preferred verbs. The second sentence is a three-beat list after an em dash, doing promotional work. The rewrite says what the reader will actually do.

---

## Marketing boast disguised as technical statement

**Before:**
> You don't need custom events — standard page views, page pings, and link clicks are enough to build meaningful real-time context.

**After:**
> Signals doesn't need custom events: standard page views, page pings, and link clicks are enough to build real-time context.

**Why:** "Meaningful" is doing promotional work. The em dash adds unnecessary drama to a straightforward technical fact. The colon is a better fit here.

---

## Promotional tail

**Before:**
> This means every Signals computed attribute you pass becomes immediately available for targeting and segmentation — no setup step in the Statsig console required.

**After:**
> Every Signals computed attribute you pass is available for targeting and segmentation. You don't need to register attributes in the Statsig console first.

**Why:** The clause after the em dash is a mini sales pitch tacked onto the end. Make it its own sentence, and say specifically what isn't needed rather than the vague "no setup step."

---

## AI compound noun + forced casual

**Before:**
> It gives your team a much richer analytical surface without any additional engineering work.

**After:**
> Your team can break down experiment results by any attribute you pass, without building anything new.

**Why:** "Analytical surface" is an AI compound noun that nobody says aloud. "Much richer" is an unsubstantiated comparative. "Without any additional engineering work" overstates — you are writing SDK code; what you're not building is infrastructure. The rewrite says what actually happens.

---

## Dramatised escalation

**Before:**
> What started as "let's segment our A/B tests better" becomes a quarter-long infrastructure investment.

**After:**
> Building segmentation pipelines from scratch can take months of engineering time.

**Why:** The "what started as X becomes Y" structure is AI dramatising a progression for rhetorical impact. The quoted inner monologue ("let's segment our A/B tests better") is a cinematic device. State the cost directly.

---

## Self-referential callback

**Before:**
> This is why the earlier tip matters: **pass all relevant Signals attributes, not just the ones you're targeting on.** It gives your team a much richer analytical surface without any additional engineering work.

**After:**
> **Pass all relevant Signals attributes, not just the ones you're targeting on.** You can then break down experiment results by any attribute, without building new pipelines.

**Why:** "This is why the earlier tip matters" is AI cross-referencing its own previous statement to build a rhetorical case. If the recommendation is worth repeating, just repeat it. Drop the meta-commentary about why your earlier point was important.

---

## Formulaic heading

**Before:**
> ## Putting It All Together - The Full Flow

**After:**
> ## The complete conversion flow

**Why:** "Putting It All Together" is an AI-default heading. It announces structure rather than describing content. Name the actual content.

---

## Unsubstantiated comparative

**Before:**
> When you connect the two, your Google Ads team gets two things it didn't have before: segmented ROAS reporting and smarter value-based bidding.

**After:**
> When you connect the two, your Google Ads team gets two new capabilities: segmented ROAS reporting and value-based bidding driven by real-time user attributes.

**Why:** "Smarter" compared to what? The comparative implies a baseline but doesn't name it. Say what makes it different instead.

---

## Flattery framing

**Before:**
> But as a business expert you already know a transaction from a high-LTV customer is worth significantly more than one from a buyer that will not revisit your site.

**After:**
> A transaction from a high-LTV customer is worth more than one from a buyer who won't return.

**Why:** "As a business expert you already know" is unnecessary framing that flatters the reader. Just state the fact. Also tightened "significantly more" (how much more?) and "that will not revisit your site" (wordy).

---

## Wrong tense for future instructions

**Before:**
> For domain-specific data like extracted travel intent or flight search parameters, you create your own custom entities and attach them alongside the generic schemas.

**After:**
> For domain-specific data such as extracted travel intent or flight search parameters, this accelerator will help you create your own custom entities and attach them alongside the generic schemas.

**Why:** At this point in the introduction, the reader hasn't created anything yet. Present tense ("you create") sounds like describing an existing system. Future tense ("you'll create" or "will help you create") is correct for instructions about what's coming.

---

## Awkward future/present tense mix

**Before:**
> The example attributes we will use in this showcase are the following:

**After:**
> This post uses the following example attributes:

**Why:** "We will use in this showcase" is an awkward mix of future tense and formal phrasing. The attributes are already defined — present tense is correct. "Showcase" is also AI-flavoured; "post" or "tutorial" is what it actually is.

---

## AI vocabulary: "divergence risk"

**Before:**
> This means double the maintenance burden, divergence risk between two event streams, and a constant game of keeping both in sync as your product evolves.

**After:**
> This means maintaining two event streams that can drift out of sync, and keeping both updated as your product changes.

**Why:** "Divergence risk" is AI-inflated vocabulary for "they can get out of sync." "A constant game of" is a forced-casual construction. "Double the maintenance burden" is vague — the rewrite says what the actual work is.

---

## Short list with filler intro

**Before:**
> A few things worth noting about this implementation:
> - `formatAttributes()` converts the raw attributes object into a markdown section ready for the system prompt
> - If Signals isn't configured or a fetch fails, the function returns an empty string — the agent degrades gracefully and still works without context

**After:**
> The `formatAttributes()` function converts the raw attributes object into a markdown section that can be appended to the agent's system prompt.
>
> If Signals isn't configured or a fetch fails, the `getSignalsContext()` function returns an empty string. The agent still works without the Signals context.

**Why:** Two items don't need a list. "A few things worth noting" is filler. The second point also contained "degrades gracefully" (jargon used to sound authoritative) and another em dash.

---

## Grandiose scope claim

**Before:**
> This tutorial walks you through instrumenting all three layers with Snowplow behavioral data tracking, progressively building from zero observability to complete transparency.

**After:**
> This accelerator walks you through instrumenting all three tracking layers with Snowplow behavioral data tracking.

**Why:** "Complete transparency" is meaningless — what does it concretely refer to? "Progressively building from zero to complete" is a marketing arc, not a technical description. Cut it.

---

## Summary that restates the introduction

**Before:**
> Signals provides the **what** — real-time computed attributes that describe each user's behaviour, value, and risk profile. Statsig provides the **mechanism** — targeting rules, experiment bucketing, variant assignment, and results analysis. Connecting the two requires no custom infrastructure: pass Signals attributes in the `StatsigUser.custom` field, define targeting rules in the Statsig console, and read experiment parameters in your code.

**After:**
> To connect Signals and Statsig: pass Signals attributes in the `StatsigUser.custom` field, define targeting rules in the Statsig console, and read experiment parameters in your code.

**Why:** The **what** / **mechanism** framing is AI imposing a tidy conceptual structure on the conclusion. Both products were already introduced at the top of the post — the summary shouldn't re-explain them. Cut to the actionable recap.

---

## End-of-page trailer

**Before:**
> Client-side tracking gives you visibility into the user's experience, but the agent's internal behavior is still invisible. When the agent receives a message, it enters a multi-step reasoning loop — calling the LLM, deciding which tools to use, executing them, and generating a response. None of that is captured yet. In the next section, you'll add server-side tracking to see inside the agent's orchestration.

**After:**
> You now have visibility into what the user does in the browser.

Or just end the page after the last substantive section — no transition paragraph at all.

**Why:** Four sentences doing the work of zero-to-one. The summary restates what the reader just learned. The preview of the next section re-sells the problem and describes what the reader can already see in the sidebar. On multi-page content, AI adds these "previously on... / next time on..." paragraphs at the end of every page. Cut them or reduce to a single short sentence at most.

---

## Forced-casual non-technical phrasing

**Before:**
> Snowplow Signals computes user attributes from your Snowplow behavioral event stream. This step gets that stream flowing.

**After:**
> Snowplow Signals computes user attributes from your Snowplow behavioral event stream. Follow these steps to create events to work with.

**Why:** "Gets that stream flowing" is AI trying to sound casual and landing on something nobody would actually say in technical documentation.

---

## AI technical verb as heading

**Before:**
> ## Wire tracking into the UI

**After:**
> ## Add tracking to the UI

**Why:** "Wire" for "connect/add" is AI-preferred vocabulary that doesn't match how the team actually talks. Use the simpler, more common verb.

---

## Bold pseudo-heading vs. inline bold term

**Before:**
> **Server-side tracking**. Server-side tracking captures events from the application backend, independent of the browser or app. It's more reliable, unaffected by ad blockers, browser privacy settings, or JavaScript execution failures, and has been best practice long before AI agents became a consideration.

**After:**
> **Server-side tracking** captures events from the application backend, independent of the browser or app. It's more reliable than client-side collection, unaffected by ad blockers, browser privacy settings, or JavaScript execution failures.

**Why:** The bold standalone sentence is a pseudo-heading — it forces the key term to be repeated immediately as the subject of the next sentence. Inline bold surfaces the term without the redundancy. Note the before version also drops the baseline for "more reliable" (more reliable than what?), which the rewrite makes explicit.
