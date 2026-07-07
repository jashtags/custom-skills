---
name: business-analysis
description: End-to-end business/product idea evaluation — market research, existing-player mapping, gap analysis, strategy, moat, target customers, launch plan, pilot design, MVP scope, PRD writing, and metrics to track. Finishes by spawning an independent critic agent to red-team the whole analysis, then revises the analysis based on that feedback before presenting a final recommendation. Use when asked to evaluate, validate, size up, pressure-test, or build a go-to-market/product plan for a business idea, feature, product, or startup concept — not for general company research with no idea to evaluate.
---

# Business Analysis: End-to-End Idea Evaluation

This is a full pipeline, not a single-pass report. Work through the phases
in order, using real research (WebSearch/WebFetch) wherever a claim needs
evidence — never fabricate a market size, a competitor's traction, or a
metric benchmark. If a number can't be found, say so and derive a
bottom-up estimate with the assumption stated in plain sight, rather than
presenting a guess as fact.

Follow `operating-playbook` for the underlying triage rules (decide vs.
ask, how to prioritize, how to write the final report). This skill is the
domain-specific content on top of it.

## Before starting: scope the idea precisely

Restate the idea as a single testable sentence before researching anything:

> **[Target customer]** currently solves **[problem]** via **[status quo /
> current alternative]**, which costs them **[the pain — time, money,
> risk, embarrassment]**. We propose **[solution]**, and believe now is the
> right time because **[why now]**.

If the target customer, geography, or B2B-vs-B2C axis is genuinely
undetermined and changes the whole analysis, ask one direct question before
going further — everything downstream depends on it. If it's just
under-specified but a reasonable default exists (e.g. assume the same
geography as the requester, assume B2B if the described buyer is a company),
state the assumption and proceed.

---

## Phase 1 — Market research (size + timing)

- **Size it bottom-up before quoting top-down numbers.** Bottom-up:
  (number of addressable customers) × (realistic price or unit economics) =
  SOM; work outward to SAM (addressable segment) and TAM (total category)
  from there. Top-down industry-report numbers are useful as a sanity
  ceiling, not as the headline figure — they're routinely inflated.
- **Search for real data**: recent market-size reports, analyst estimates,
  adjacent-company revenue disclosures, funding rounds in the space (funding
  velocity is a decent proxy for investor belief in market timing).
- **Establish timing ("why now")** explicitly: what changed recently that
  makes this newly viable or newly urgent — a technology cost curve, a
  regulatory shift, a behavior change, a platform opening up, a recent
  failure of an incumbent. An idea with no "why now" answer is either too
  early or has already had its window.
- **Note the trend direction** (growing / flat / shrinking) — a small
  fast-growing market often beats a large flat one for a new entrant.

## Phase 2 — Existing players / competitive landscape

- **Map three tiers**, not just direct competitors:
  1. **Direct** — same solution shape, same target customer.
  2. **Indirect** — different solution, same underlying job-to-be-done
     (including manual/DIY workarounds).
  3. **Status quo / do-nothing** — very often the real competitor, especially
     in B2B. If switching cost from "doing nothing" isn't addressed, the
     rest of the analysis doesn't matter.
- **For each real competitor**, pull (via search, not memory): pricing
  model, target segment, apparent traction/funding signal, and its most
  visible weakness (from reviews, complaints, churn signals, or gaps in
  their own marketing claims).
- **Build a two-axis positioning map** using the two dimensions the target
  customer actually cares about (not generic axes like "quality vs. price"
  unless that's genuinely what's decisive) — plot where the incumbents sit
  and where the open space is.

## Phase 3 — Gap / whitespace analysis

Look for gaps in three categories and rate each on size × reachability:

- **Underserved segments** — a customer type competitors ignore or serve
  poorly (wrong price tier, wrong company size, wrong geography, wrong
  workflow).
- **Unmet needs within served segments** — feature gaps, price-point gaps,
  experience/quality gaps visible in complaints and reviews of incumbents.
- **Structural gaps** — a distribution channel, business model, or
  technology approach nobody in the space has tried.

Be honest about gap size: a gap only matters if it's big enough to build a
business on and reachable with a realistic go-to-market motion. A real but
tiny gap is a feature request, not a company.

## Phase 4 — Strategy and differentiation

- **Pick a generic strategy lens** (Porter): cost leadership, differentiation,
  or focus/niche — pick one primary lens; trying to win on all three usually
  means winning on none.
- **Default to a wedge strategy** for anything new: win a narrow beachhead
  segment completely before expanding, rather than launching broad and thin.
  State explicitly what the beachhead is and what the second and third
  markets are once the beachhead is won.
- **Name the business model**: subscription, transaction/take-rate,
  usage-based, freemium-to-paid, advertising, licensing — and why that model
  fits how the target customer already prefers to pay in this category.
- **Write the positioning statement**:

  > For **[target customer]** who **[need/pain]**, **[product]** is a
  > **[category]** that **[key benefit]**. Unlike **[primary alternative]**,
  > we **[key differentiator]**.

## Phase 5 — Moat / defensibility

Rate each candidate moat as *present now*, *buildable*, or *not applicable* —
don't claim a moat that's really just a feature (copyable in weeks):

| Moat type | Present at launch? | How it's built over time |
|---|---|---|
| Network effects | Rarely | Grows with user count/interconnection |
| Data / learning effects | Rarely | Compounds with usage volume |
| Switching costs | Sometimes (integration depth) | Grows as customer embeds the product in their workflow |
| Brand | Rarely | Built over years of consistent delivery |
| Economies of scale | Rarely at small size | Unlocks as volume grows |
| Proprietary tech / IP | Sometimes | Defensible only if genuinely hard to replicate |
| Regulatory / licensing barrier | Sometimes | Fixed at market entry, doesn't grow |
| Exclusive distribution/partnership | Sometimes | Depends on the partner relationship |

Most early-stage ideas have **no moat on day one** — the honest answer is
usually "we out-execute and compound one of these over time," and the
analysis should say that plainly rather than inventing a moat that doesn't
exist yet.

## Phase 6 — Target customers

- **Define the ICP** (Ideal Customer Profile): firmographic/demographic
  traits + behavioral traits + pain intensity signal (how they currently
  spend money/time solving this).
- **Frame the job-to-be-done**: functional job (the task), emotional job
  (how they want to feel), social job (how they want to be perceived) —
  a product that only addresses the functional job is easier to displace.
- **Prioritize segments** by scoring pain intensity × willingness to pay ×
  reachability × segment size, and name the single beachhead segment this
  plan optimizes for first.

## Phase 7 — Go-to-market / launch strategy

- **Sequence it** (bowling-pin strategy): beachhead segment first, then the
  adjacent segment it unlocks, then the broader market — name the actual
  sequence, don't launch to "everyone."
- **Pick 1-2 channels**, matched to how the target customer actually
  discovers and buys in this category (content/SEO, paid acquisition,
  outbound sales, product-led self-serve, partnerships/integrations,
  community, marketplace listing) — trying every channel at once dilutes
  all of them.
- **Set launch pricing strategy** explicitly: penetration (low price to
  capture share fast), premium (signal quality, filter for serious buyers),
  or freemium (low-friction top of funnel, monetize a subset) — and why that
  fits the business model and competitive position from Phase 3.

## Phase 8 — Pilot design

- **Identify the single riskiest assumption** to test before building
  anything substantial — usually "will someone actually pay for this" or
  "will they use it more than once," not a technical risk.
- **Design the cheapest test that would falsify the assumption**: a
  concierge MVP (manually deliver the outcome), a Wizard-of-Oz test (fake
  the automation, deliver it by hand), a landing page + waitlist with a real
  payment/commitment step, or a paid pilot with a handful of real customers.
- **Set numeric success criteria before running it** — "X% of pilot users
  convert to paid" or "Y customers complete the core action Z times in two
  weeks" — not "see how it goes." A pilot without a pre-committed threshold
  can't fail, which means it can't teach anything.

## Phase 9 — MVP scope

- Define the MVP as **the smallest thing that tests the pilot's riskiest
  assumption** — not "version 1 with fewer features." If a feature doesn't
  affect whether the pilot's success criteria can be measured, it's out of
  scope for the MVP by definition.
- Identify the **one core loop** the product must deliver end-to-end;
  everything else (settings, edge cases, polish, secondary user types) is
  explicitly deferred and should be named as deferred, not silently dropped.
- Consider **build vs. buy vs. no-code** for the MVP itself — the MVP's job
  is to produce a learning, not to be defensible or scalable code; over-
  engineering it wastes the exact time it exists to save.

## Phase 10 — Writing the PRD

Once the MVP scope is set, write it up in this shape:

1. **Title + one-line summary.**
2. **Problem statement** — who, what pain, current alternative, cost of
   the status quo (reuse Phase-0 framing).
3. **Goals** (what this ships to achieve) **and non-goals** (explicitly out
   of scope, to prevent scope creep later).
4. **Target users** (from Phase 6's ICP/beachhead).
5. **User stories / core use cases** — as concrete flows, not abstractions.
6. **Requirements** — functional (what it must do) and non-functional
   (performance, reliability, compliance constraints that matter here).
7. **Success metrics** (from Phase 11) with the specific target values.
8. **Risks and open questions** — named explicitly, not buried in prose.
9. **Milestones / rough timeline.**

If the build phase follows, hand off to `software-development-sdlc` for the
actual implementation planning — this PRD is the input to that process, not
a replacement for it.

## Phase 11 — Metrics to track

- **Pick one North Star Metric**: the single number that best represents
  value actually delivered to the customer (not a vanity metric like page
  views or signups) — e.g. "weekly active teams completing the core
  workflow," not "total registered users."
- **Map the funnel** relevant to the business model (a common shape:
  Acquisition → Activation → Retention → Referral → Revenue) and pick one
  or two metrics per stage.
- **Separate leading from lagging indicators** — leading metrics (activation
  rate, time-to-first-value) predict the lagging ones (retention, revenue)
  early enough to act on.
- **Stage-appropriate metrics**:
  - Pre-launch/pilot: qualified waitlist signups, pilot conversion rate,
    pilot task-completion rate.
  - Early post-launch: activation rate, Week-1/Week-4 retention curves,
    qualitative feedback (NPS or direct interviews) — not CAC/LTV yet, the
    sample is too small to trust those numbers.
  - Growth stage: CAC, LTV, payback period, retention cohorts, channel-level
    conversion.

---

## Phase 12 — Red-team the analysis with a spawned agent (required step)

Once Phases 1–11 produce a first draft, **do not treat it as final.** Use
the Agent tool to spawn a **fresh, non-fork agent** — not a fork — because
the point is an independent perspective that isn't anchored on the
reasoning that produced the draft. A fork inherits your context and your
biases; a fresh agent doesn't, which is exactly what a red-team needs.

1. **Brief the fresh agent as a skeptical, specific critic** — an investor
   doing diligence or a devil's advocate operator, not a generic reviewer.
   Give it the full draft analysis (it has no memory of this conversation,
   so paste in the market sizing, competitive map, gap claim, moat claim,
   ICP, GTM plan, pilot design, and metrics — everything it needs to attack
   is everything it's given).
2. **Ask for concrete, falsifiable objections**, explicitly across these
   angles, not a generic "this might not work":
   - Is the market-size number credible, or does it quietly assume
     unrealistic capture?
   - Is the "gap" real, or is it a gap for a reason (regulatory,
     unit-economics, a reason incumbents already tried and abandoned it)?
   - Is the claimed moat genuine, or copyable by a competitor in weeks?
   - Is the target customer specific enough to actually reach, or is it
     "everyone who has this problem"?
   - Are the pilot's success criteria strict enough to actually falsify the
     idea, or are they set up to pass?
   - Are the chosen metrics real signals of value, or vanity metrics?
   - What's the single assumption that, if wrong, breaks the whole plan?
3. **Take the critique seriously and revise the actual document** —
   for each substantive objection, either change the recommendation/plan
   to address it, or write an explicit rebuttal backed by evidence. Do not
   append the critique as an unaddressed footnote; the final deliverable
   should read as already having absorbed it.
4. **Run a second round** only if the first critique surfaces something
   that invalidates a core assumption (not for objections already handled
   by a straightforward revision) — don't loop indefinitely.

## Phase 13 — Final deliverable

Structure the output so the recommendation is visible immediately, details
after (see `operating-playbook` §7 — lead with the conclusion):

1. **Executive summary**: go / no-go / pivot-and-retest, in one paragraph,
   plus the single biggest risk.
2. **Condensed findings** from each phase — a few lines each, not the full
   working.
3. **What the red-team critique changed** — the specific points that altered
   the plan, briefly.
4. **Next steps**, concretely sequenced (e.g. "run the pilot with N
   customers over 4 weeks against these thresholds before writing any
   production code").

For a substantial analysis, offer to render the final deliverable as an
Artifact (a clean, shareable page) rather than a long chat wall of text —
ask only if it's genuinely long enough to benefit; a short verdict doesn't
need one.
