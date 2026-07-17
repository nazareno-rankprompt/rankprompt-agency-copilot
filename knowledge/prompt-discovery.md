# Prompt discovery — finding the right questions to track

You can't improve visibility for questions you never measure. This is how to build a prompt set that reflects what your buyers actually ask AI.

## Start from the buyer, not the brand

Begin with **who actually buys and what makes them start looking** (their "ideal customer" — but don't use jargon like *ICP* with the user; ask it plainly). A 2-person startup buying a CRM asks different questions than an enterprise IT director. Their questions become your prompts.

**Use the buyer's words, not yours.** Car buyers search "buy here pay here", not "in-house financing". Planners search "silent conference", not "silent disco". If your prompts use brand/industry jargon instead of buyer language, the whole report measures the wrong thing.

## Cover the seven kinds of question

Real buyers move through stages. Spread your prompts across them so you see the whole funnel:

| Intent | Example |
|---|---|
| Awareness | "what is {topic}?" |
| Educational | "how does {topic} work?" |
| Comparison | "{Brand} vs {Competitor}" |
| Alternatives | "{Competitor} alternatives" |
| Consideration | "{Brand} reviews / pricing" |
| Purchase-intent | "best {topic} for {need}" |
| Use-case | "{topic} for {persona}" |

Purchase-intent and comparison/alternatives are where buyers are closest to choosing — weight toward them, but don't skip the top of the funnel.

## Template by location for multi-market brands

If geography drives the buy, write the prompt once with a slot — `best {category} in {location}` — and expand `{location}` across your markets. Identical prompt sets across markets are what make markets *comparable* (why you win one city and not another). Don't hand-write fifty near-duplicates.

## Auto-generate vs. hand-author

- **Auto-generate** (the API can do this) to cover a category quickly and broadly.
- **Hand-author** when you need a precise buyer question, a specific competitor comparison, or tricky vocabulary.

Use both. A good working size is about **12–15 prompts per market** — enough to be representative, small enough to compare run to run.

## Harvest the answers

After you run a report, read the **actual answers** AI gave (see `reading-reports.md`) — the sub-angles, comparison dimensions, and brands each answer raises are the model's own breakdown of each topic, which makes them high-confidence new prompts and categories to add next round.

## What a good prompt set looks like

- Real questions a real buyer would type.
- Balanced across the seven intents.
- In the buyer's vocabulary.
- Market-aware (templated by location if relevant).
- Grounded in your actual category — not vanity prompts you'd *like* to rank for.

Once you have the set, the copilot creates the report, adds the prompts, runs it, and you read the result (`reading-reports.md` → `brain.md`).
