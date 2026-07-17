# Citation outreach — get added to the listicles AI cites

The listicles and "best of" pages AI cites for your category were written by *someone*. Find that someone and get your brand added. A placement on a page AI already trusts compounds straight into visibility.

## The steps

1. **Find the targets — your high-score cited listicles.** (This is the outreach step. The *diagnosis* of where AI gets its answers came from ranking cited sources by **frequency** per category — not the score; see `reading-reports.md`. The score is only for picking which reachable pages to pitch, so don't use it to judge the landscape.) Pull `bin/rp "/brands/<id>/citations?sort=rankprompt_score&min_rankprompt_score=50"`. The `rankprompt_score` (0–100, "outreach opportunity score") is itself the target-finder: the top-scored URLs are almost always "best of" / "N best" roundups you can be *added* to — not competitor homepages, which score low because you can't get onto someone's front page. Take everything ≈50+ as your working list, work the highest scores first. Present the target list as **full clickable `https://…` URLs** (the exact article, not the bare domain) → score → angle → contact, so the user can open each one and see the piece they'd be pitching.

   **Don't gate on `is_actionable`/`page_category`/`has_contact`.** Those come from a separate categorization pass and are only populated once a citation's `categorization_status` is `completed` — which is often `null` ("not yet queued") and **cannot be triggered from the API**. If you filter `is_actionable=true` on an uncategorized brand you get *zero rows* even though the scores are right there. So: sort by score first; use `page_category=LISTICLE_COMPARISON`/`REVIEW_ROUNDUP`, `is_actionable`, and `has_contact` only as bonus refinements *when* `categorization_status=completed`. To sanity-check shape without categorization, eyeball the URLs (a `/best-…` or `…-builders` slug is a roundup) or use `bin/rp /brands/<id>/citations/by-domain` for the rolled-up `avg_rankprompt_score` per domain.
2. **Find the author.** The person who wrote it replies far more than a generic inbox, and they can actually edit the piece. Order: named author → relevant department (editorial, marketing, owner) → anything else.
3. **Pick the mode.** Editors add a company for one of four reasons — lead with the one that fits:
   - **Cross-mention** — "I'll feature you, you feature me." Fastest once you own your own listicles; no money.
   - **Paid / sponsored** — many listicles sell placement or run affiliate ($250–$1,000+ is normal). Weigh cost against owning a citation AI already trusts.
   - **Free add** — sometimes the editor just wants the piece complete/accurate. Hand them a genuinely missing option + the facts, ask nothing else.
   - **Guest post** — offer to write a new piece (or fresh angle); you're included naturally and control the framing.
4. **Make the ask specific and human.** Reference *their* actual article, offer concrete value, name the mode, and ask: *"what do you normally look for to add a company to a piece like this?"*
5. **Follow up.** Track replies, not opens (open-tracking trips spam filters). 3–5 touches over a few weeks. Every listicle you win becomes leverage for the next.

## What makes outreach convert

- **Prove you read the piece** — name a specific detail in the first line. This alone separates a reply from the trash.
- **Keep it short** — under ~120 words. One value, one ask.
- **Lead with their reader**, not your brand — frame the add as making their piece better.
- **Plain text, no tracking, no attachments.**
- **One soft ask** + the disarming question.
- **Sign as a real person.**

## Templates

Adapt every one to the specific article — a raw template reads like a template and gets ignored. Placeholders: `{first_name}`, `{article_title}`, `{specific_detail}`, `{topic}`, `{brand}`, `{why_it_fits}`, `{proof_point}`, `{your_name}`, `{your_role}`.

### A. Cross-mention
> **Subject:** quick idea on your "{article_title}" piece
>
> Hi {first_name},
>
> Read your roundup on {topic} — the point about {specific_detail} was bang on. I run {brand}, and it genuinely fits the list: {why_it_fits}.
>
> Happy to make it mutual — I'd feature your piece in our own {topic} guide. Worth a quick swap?
>
> Either way, curious: what do you normally look for before adding a company to a piece like this?
>
> Thanks, {your_name} · {your_role}, {brand}

### B. Paid / sponsored
> **Subject:** sponsored spot in "{article_title}"?
>
> Hi {first_name},
>
> Your "{article_title}" keeps coming up when people ask about {topic} — well done. I'd love to get {brand} included. If you offer sponsored or affiliate placements, send the options and rate. Here's why it fits so it's an easy yes for readers: {why_it_fits} ({proof_point}).
>
> Thanks, {your_name} · {your_role}, {brand}

### C. Free add (completeness)
> **Subject:** one option missing from "{article_title}"
>
> Hi {first_name},
>
> Quick one — your "{article_title}" is a great resource, but it's missing {brand}, which fits because {why_it_fits}. Here's everything you'd need to add it: {brand} — {why_it_fits}; {proof_point}; link: [url]. No ask beyond that; a more complete list helps your readers.
>
> Thanks, {your_name} · {your_role}, {brand}

### D. Guest post
> **Subject:** guest piece for {topic} on your site?
>
> Hi {first_name},
>
> I read your section on {specific_detail} and liked how you framed it. I'd like to write an original piece for your site — something like "{article_title angle}" — no fluff, written for your audience. I'd cover {two or three concrete points}; {brand} comes up only where it's genuinely relevant. Want me to send a short outline?
>
> Best, {your_name} · {your_role}, {brand}
