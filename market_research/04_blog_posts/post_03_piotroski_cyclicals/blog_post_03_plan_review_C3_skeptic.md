# Skeptic Review — Blog Post #3 Plan
**Reviewer**: C3 (Quant / Investing Skeptic)
**Date**: 2026-05-31
**Reviewed artifact**: `blog_post_03_plan.md`

---

## §1 — Skeptic Verdict

**Verdict: NEEDS-WALK-BACK** (with structural reconstruction in §5)

The post makes a falsifiable claim — "the F-Score is anti-correlated with cyclical entry opportunity" — and anchors it on N=4 data points from a single stock over a ~4-year window. That is not a weak finding with caveats; it is an anecdote. A well-reasoned anecdote with a mechanistic explanation behind it, but an anecdote still. The plan's "Risks / things to watch" section already identifies this ("One-stock evidence") but then proposes a hedge that is too weak to survive a technically literate reader in the comments: *"I tested it on one stock at 4 dates. That's not statistical proof. But the pattern lines up with how cyclicals work in theory, so I think the finding will hold."* That sentence is how post-hoc rationalization sounds when dressed in humility.

The good news: the mechanistic argument (coincident vs. leading indicator on mean-reverting assets) is independently strong and does not depend on the N=4 evidence at all. If the post restructured around the mechanism and used the Tata Steel data as illustration rather than proof, most of these objections collapse. What I'm flagging below is specifically what the current draft structure enables a skeptic to attack.

Seven problems follow, in order of severity.

---

## §2 — Per-Question Skepticism

### Q1 — One-stock, four-dates evidence: N=4, selection bias risk is high

The core of §3 is four rows in a table. Every single row is Tata Steel. The author chose Tata Steel because they already hand-computed it for Cycle A of their analytical system. That is not neutral sampling — it is picking the stock for which you already have data, which is likely the stock that motivated your hypothesis in the first place.

The selection bias scenario the post does not rule out: the author tried F-Score on several cyclicals, Tata Steel showed the inversion clearly, other cyclicals were messier, and Tata Steel ended up as the example because it was the cleanest. The post has no way to refute this without showing it explicitly tested other cyclicals and found the same or a similar pattern.

The four dates are also not independent observations. March 2020, March 2021, March 2022, and March 2024 are all drawn from the same stock's life, during the same global macro episode (COVID, the commodity supercycle, the post-supercycle normalization). A skeptic can argue all four data points describe one event, not four.

**What the post needs to do**: The "still learning, not done" tone is the right direction but the hedge as currently phrased ("I think the finding will hold") is overconfident given N=1 stock. The honest statement is: "I have exactly one data series. I cannot rule out that Tata Steel is the exception, not the rule, among Indian cyclicals." The post should invite readers with data on other metals/fertilizer/cement stocks to test and report back — and frame this as active crowdsourcing, not a defensive disclaimer.

---

### Q2 — The anti-correlation claim needs a statistical spine, or the word "anti-correlated" needs to disappear

The plan instructs that technical vocabulary like "anti-correlation" is for internal documents only, and the blog uses plain English ("the opposite"). That is the right call for audience clarity. But the underlying problem does not disappear by renaming it.

The post is making a directional statistical claim: when F-Score goes up for cyclicals near turning points, forward returns go down. With four data points, you cannot compute a Spearman rank correlation that is statistically significant. You need at minimum 8-10 data points to get any meaningful p-value from a Spearman test, and even then you have autocorrelation problems because the observations are from the same stock.

The plan says to avoid "Spearman correlation" as wording. Fine. But the post's claim, translated into testable English, is: "For cyclical stocks, a higher F-Score at any given date predicts lower forward returns." That claim needs evidence beyond four rows. As written, the claim is untestable from the data presented, which makes it rhetoric, not analysis.

**What the post needs to do**: Downgrade the claim from directional-and-falsifiable to observational. The honest framing: "In the four dates I tested on this one stock, the direction was the opposite of what the F-Score predicts. This matched what I expected from the theory. But four rows from one stock cannot tell you whether this pattern holds across cyclicals generally." Then the post offers the mechanistic explanation as the durable argument, not the data pattern.

---

### Q3 — Mar-2020 is doing a lot of work, and it is not doing what the post thinks

The +355% forward return from March 2020 is the headline number. It anchors the entire "F-Score was most wrong when opportunity was highest" argument. But March 2020 was a once-in-a-generation dislocation. Every asset class — equities, commodities, even parts of fixed income — was mispriced in March 2020. The Nifty 50 itself recovered roughly 100% from its March 2020 lows to March 2022. Tata Steel returned 355%; the market returned ~100%. The F-Score did not predict the market recovery either.

The post attributes the F-Score's failure at March 2020 to cyclical-specific logic: "F-Score sees the cycle bottom and calls it weak fundamentals." That explanation is plausible. But an equally valid explanation for the +355% is: "everything was cheap in March 2020, and leveraged cyclicals with operational leverage gave 3-4x the market return in the recovery — as they always do from COVID lows." The F-Score's failure here might be a failure to read the macro bottom, not a failure specific to cyclical stocks.

Put differently: would a high-quality, non-cyclical stock with an F-Score of 5 in March 2020 also have massively outperformed its F-Score prediction? Quite possibly. The post does not address this. Without that counterfactual, the Mar-2020 data point does not cleanly support the cyclical-specific argument.

**What the post needs to do**: Acknowledge that March 2020 was a global macro event and that the cyclical-specific argument is harder to isolate for that specific data point. The cleaner evidence for the cyclical argument is March 2021 (F=8, +34%) and March 2022 (F=7, ~0%) — where the F-Score was high and the stock was at or past the cycle peak. Those two data points do not carry a COVID-dislocation explanation. The post should lean on those two, not on March 2020.

---

### Q4 — Stock Y: "illustrative numbers if data is messy" is a problem

The plan explicitly says: "If Asian Paints' specific numbers don't tell a clean 'F-Score worked' story across the dates we have data for, fall back to illustrative numbers in §5 — the pattern is what matters, not the exact figures."

This is intellectually uncomfortable, and a skeptic in the comments will find it immediately.

The post's argument structure requires a positive control: Stock Y shows the F-Score working. If Stock Y's empirical data doesn't actually show that, and the author substitutes illustrative numbers, the entire contrast in §5 becomes a hypothetical. The post is then arguing: "Here is a real case where the F-Score failed [Stock X — one stock, four dates]. Here is a made-up case where the F-Score worked [Stock Y — illustrative]. Therefore the F-Score fails specifically on cyclicals."

That inference is not valid. You cannot compare a real failure against a hypothetical success and draw a conclusion about the failure mode. If the author tested the F-Score on only cyclicals (or only on "the stock that motivated the hypothesis"), and has no real empirical success case, the post is confirming a negative with no positive control.

**What the post needs to do**: Either produce real Stock Y data — hand-computed, dated, with actual forward return outcomes — or explicitly label §5 as theoretical rather than empirical. If it is labeled theoretical, the section still has value as a "here is how the F-Score would behave on a stable business, and here is why the math suggests it should work" section. But it cannot carry the weight of an empirical contrast.

---

### Q5 — "Piotroski never said this was for cyclicals" is factually incomplete

§4 claims: "It's not that Piotroski is wrong. It's that he never said this was for cyclicals." This is partially accurate but incomplete in a way that a technically literate reader will challenge.

Piotroski (2000) filtered the universe to high book-to-market (B/M) stocks — value stocks. Cyclical companies at the bottom of their cycle frequently trade at distressed valuations with high B/M ratios (depressed price relative to book). Tata Steel in March 2020, which the plan calls a "cycle trough," was almost certainly trading at a high B/M ratio — exactly the universe Piotroski was targeting.

This creates a direct counter-argument: Piotroski's design actually does cover cyclicals at troughs, because cyclicals at troughs look like distressed value stocks by B/M ratio. If Piotroski's paper found that high F-Scores within the high-B/M universe predicted outperformance, and if Tata Steel in March 2020 was in the high-B/M universe with a mid-level F-Score of 5, then the question is not "was this the intended application" but "did the empirical relationship Piotroski found fail to hold in this instance." That is a much harder and more specific claim.

The post as planned sidesteps this by saying Piotroski designed it for "value stocks" and cyclicals are different. But cyclicals at troughs ARE high-B/M value stocks. The categories overlap precisely at the moment the post claims the F-Score is most wrong.

**What the post needs to do**: Address the B/M overlap directly. The honest position is: "Cyclicals at cycle troughs often look like the high-B/M stocks Piotroski was studying — but within that universe, the F-Score signal still fires at the wrong time for cyclicals because the B/M is elevated due to price collapse, not because the underlying business is permanently distressed. The recovery of a cyclical is a cycle recovery, not a value realization. Piotroski's alpha came from separating genuinely improving distressed businesses from deteriorating ones — cyclicals at troughs are genuinely deteriorating by every YoY metric, which is why the F-Score is low, and they will still recover because the cycle turns." This is actually a stronger and more precise argument than "Piotroski never said this."

---

### Q6 — The 5-year-average fix (§6): a different guess, not a validated fix

§6 proposes switching from year-on-year comparisons to 5-year-average comparisons to smooth the cycle. The plan presents this as "it's not perfect, but it's better." Better by what standard? Against what baseline? With what evidence?

The plan offers no evidence that the 5-year-average version of the F-Score produces better entry signals for cyclicals. "5 years" is an arbitrary choice. Why not 3 years, which might match the length of a specific commodity cycle? Why not the average of the prior full cycle peak-to-trough? Commodity cycles have variable lengths — the steel cycle in India has been structurally different across 2003-2008, 2012-2016, and 2020-2024 periods. A fixed 5-year window will straddle cycle turns differently depending on when you measure.

The risk of presenting an untested alternative in a blog post: readers implement it. If the 5-year-average F-Score has its own failure modes (which it will — any mechanical rule does), the author has recommended something with unknown properties. This is worse than recommending nothing.

**What the post needs to do**: Be explicit that the 5-year-average modification is a hypothesis, not a tested improvement. "I changed the comparison window. I have not backtested whether this actually improves the signal for cyclicals across multiple stocks and multiple cycles. This is what I'm trying next, not what I'm recommending." That is an honest framing. Presenting it as the "what I do instead" improvement implies validation that does not yet exist.

---

### Q7 — The TA "cyclical inversion" finding: should it be in the blog?

The Cycle B synthesis (referenced in the project's CLAUDE.md as a cross-cycle finding) apparently found that technical analysis has the same inversion pattern for cyclicals. This is potentially the most valuable supporting evidence for the blog's core claim — it would show that the anti-correlation at cycle turns is not specific to the Piotroski score but is a property of any backward-looking indicator applied to mean-reverting assets.

The plan excludes this because the blog is about FA specifically. That is a defensible editorial choice. But excluding it has a cost: the post's argument rests entirely on N=4 from one stock, when the author apparently has corroborating evidence from an independent analytical framework that shows the same structural inversion. The decision to keep it out, while keeping the weak one-stock evidence, is an odd tradeoff.

**What the post needs to do**: If the TA inversion finding is available and credible, include a one-sentence reference. Something like: "When I tested technical momentum signals on the same stock, I found the same inversion — momentum was lowest at the entry point and highest at the peak. This made me more confident the pattern I was seeing in the F-Score wasn't a coincidence specific to that checklist." This does not make the blog about TA. It uses TA as a cross-validation of the FA finding and makes the N=4 evidence materially less fragile.

---

## §3 — Specific Claims That Need Hedging or Sourcing

The following sentences, as planned, would not survive scrutiny from a technically literate reader. Each needs either a revision or explicit in-text hedging.

**Claim 1** (§4 prose): *"By the time the F-Score is telling you 'things are improving', the smart money has already bid up the stock."*
Problem: This asserts market efficiency specifically for cyclical stocks at cycle turns. This is an empirical claim about information diffusion and institutional behavior. It may be true, but it is not sourced, and it is doing real work in the argument. Without it, the "why" explanation in §4 has a gap.
Fix: Hedge to "in the case I looked at, the price had already moved substantially before the F-Score turned positive." Do not generalize to "smart money" behavior.

**Claim 2** (§3, implied by the table): *"+355% over 24 months from March 2020."*
Problem: This number needs to be verifiable. If the reader checks and the Tata Steel return from March 2020 to March 2022 is materially different, the whole post is compromised. What index date is used? BSE/NSE adjusted closing? Is this price return or total return (including dividends)? Steel companies often pay variable dividends during cycle peaks.
Fix: State the data source, the specific price dates, and whether dividends are included. One line in a footnote or a parenthetical is enough.

**Claim 3** (§4): *"The original paper was about value stocks. The Indian investing community quietly extended it to all stocks. That extension is where the problem lives."*
Problem: "The Indian investing community quietly extended it" is stated as fact. Which books, screeners, or commentators made this extension? If unnamed, this is a strawman. The post is arguing against an unspecified claim.
Fix: If the post's audience is "people who read Saurabh Mukherjea" — cite specifically whether Mukherjea's work applies Piotroski to cyclicals without caveats. If the author has seen a specific screener or book do this, say so. If not, the sentence should be "some applications of the F-Score in Indian investing don't distinguish between cyclical and non-cyclical stocks — including some tools I've used."

**Claim 4** (§5b, implied): *"For FMCG, IT services, private banks, pharma — most of NIFTY 100 — the F-Score works closer to as intended."*
Problem: "Based on what I've tested so far" is the only hedge on a sweeping sector-level claim. The author has tested Asian Paints (one FMCG stock) and Tata Steel (one metal stock). The claim covers FMCG, IT, private banks, and pharma. This is a massive overgeneralization from N=1 positive control.
Fix: Cut "most of NIFTY 100" and replace with: "for the non-cyclical stock I tested, the F-Score moved in the expected direction." Do not generalize to sectors not tested.

**Claim 5** (§6): *"It's not perfect. But it's better than the textbook version for this class of stock."*
Problem: "Better" implies some comparison was made. Has the 5-year-average F-Score actually been computed and back-compared against the standard F-Score for Tata Steel (or any cyclical) to show it gives better entry signals? If not, "it's better" is speculation.
Fix: Replace with "I think it might be better, but I haven't tested that yet. It smooths the cycle mathematically; whether it actually improves entry timing is something I want to test with more data."

---

## §4 — What the Post Does Support Well Empirically

To be fair: several things in this plan are on solid ground and do not need defense.

**The mechanism is independently valid.** The core logical argument — that a year-on-year improvement signal is a coincident indicator for mean-reverting assets, not a leading one — is correct by construction. You do not need Tata Steel data to defend this. Any textbook treatment of cyclical industries explains why trailing fundamentals peak at cycle peaks and trough at cycle troughs. This argument stands without the N=4 table.

**The March 2021 and March 2022 data points are the cleanest.** These two rows — F=8 with +34% return, F=7 with ~0% return — are not confounded by the COVID global dislocation. If the cycle-peak argument has clean evidence, it lives here. These are more defensible than March 2020 because the alternative explanation (everything was cheap in COVID) does not apply.

**The "still learning" tone is structurally correct for this evidence level.** The plan locks this in as a tone requirement. That is the right call. If the post were written with the certainty its hook implies, a single commentator with data on a second cyclical stock that shows a different pattern could undermine the entire piece. The humble framing converts potential refutations into contributions to an ongoing inquiry. This is smart.

**The "cyclical stock checklist" in §5b is useful regardless of the empirical gaps.** Even if the F-Score claim does not hold up statistically, the list of stock categories where year-on-year signals are likely to be distorted by cycle position (metals, oil & gas, fertilizers, infrastructure) is a useful heuristic for readers. This section provides value independent of whether the Tata Steel data is convincing.

**The core structure of the post is repairable.** Nothing in the above requires scrapping the post. The mechanism argument is strong. The Tata Steel data is illustrative even if not statistically sufficient. The two cleanest data points (March 2021 and March 2022) are legitimately argued. With the right hedging, the tone adjustment on the "fix" in §6, and either real Stock Y data or an explicit theoretical framing for §5, this post becomes defensible. The problem is not the idea. The problem is that the current plan presents an illustrative case as if it were empirical proof.

---

**Total claims flagged**: 12 (7 structural, 5 specific)
**Verdict**: NEEDS-WALK-BACK — the mechanism is strong; the evidence framing is overextended.

`✅ Skeptic review complete. 12 claims flagged.`
