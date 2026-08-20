# The Prompt Ladder

**Arpit Joshua Elias** | General AI Fluency, Week 2

Subject: a median-CTR-by-position-decile table from my ML track work (w02_ml_task_framing).
Each version was run in a fresh chat with no project instructions, one layer added at a time.

---

## Baseline

**Prompt:** "Explain this data" plus the raw decile table, nothing else.

**Output (excerpt):** Read it as a decile lift table of positive rates. Computed a base rate of 0.153, lift of 1.9x on decile 0, and estimated 19% of positives captured in the top decile.

**Notes**
- *What changed:* nothing, this is the baseline.
- *What improved:* n/a.
- *What failed:* it guessed the frame and guessed wrong. The values are median CTR percentages, not positive rates. Every number in its lift calculation is built on a misreading it had no way to detect.
- *What next:* tell it what the numbers actually are.

---

## Version 1: real context

**Layer added:** what the dataset is, the unit of analysis, the filter applied, what CTR means, which end of the deciles is best.

**Output (excerpt):** The 0.00 in decile 9 means over half those pages got zero clicks across 90 days despite clearing 100 impressions. The 0.17/0.16/0.15/0.14 stretch is likely one click of difference on the median page. Also flagged that deciles are equal-count, not equal-position, so the x-axis has no scale.

**Notes**
- *What changed:* real context.
- *What improved:* the invented frame disappeared. The lift arithmetic is gone entirely and replaced with observations that are actually about my data. The zero-click reading of decile 9 is something I had not noticed myself.
- *What failed:* seven or eight critiques at equal weight, no ordering, no indication which matter for my decision. Long.
- *What next:* say who is asking and what the output is for.

---

## Version 2: defined audience

**Layer added:** "I'm an ML intern framing a scoring task, defending these choices to a reviewer who will push on whether my framing is honest."

**Output (excerpt):** Opened by arguing at length that my units were mislabelled, that 0.29 must be 29% rather than 0.29%, and that I should fix this before presenting anything.

**Notes**
- *What changed:* defined audience.
- *What improved:* sharper statistical vocabulary. Named decile 9 as a censored mass at zero rather than a small number, and pointed out that this breaks anything multiplicative: cannot log it, cannot use it as a denominator, cannot quote a percentage change from it.
- *What failed:* **this version made it worse.** Its headline claim was confidently wrong. I had already verified in code that CTR is a percentage, `np.allclose(clicks/impressions*100, ctr)` returns True, and median clicks of 1 against median impressions of 731 confirms the scale. Priming it for a hostile reviewer made it manufacture an objection. The baseline and version 1 did not make this error. I only caught it because I had run the check myself.
- *What next:* hand it what I have already verified so it stops re-litigating settled facts.

---

## Version 3: stated assumptions

**Layer added:** a block of facts already confirmed in code, marked do-not-re-derive.

**Output (excerpt):** Proposed that the gradient may be an impressions gradient rather than a CTR gradient. With median clicks at 1, every decile median from 0 to 8 is consistent with a single click over a growing impression base: 0.29% implies ~345 impressions, 0.06% implies ~1667.

**Notes**
- *What changed:* stated assumptions.
- *What improved:* the unit dispute vanished and the effort went somewhere new. It produced a falsifiable alternative hypothesis rather than a list of concerns, and a one-sentence claim I could defend as written.
- *What failed:* still no priority ordering, still essay-length. And confident enough now that I need to check its arithmetic rather than trust it.
- *What next:* constrain the format.

---

## Version 4: specified output format

**Layer added:** three bullets on what the table supports, three on what it doesn't, one pasteable sentence, under 200 words.

**Output (excerpt):** Structured as requested, ending with a notebook line: median per-page CTR falls monotonically from 0.29% to 0.00% across avg_position deciles, but click integrality dominates the scale and the filter conditions on impressions, so treat as ordinal only.

**Notes**
- *What changed:* specified output format.
- *What improved:* it prioritised. Version 3 gave me seven concerns at equal weight and left the ranking to me. This one committed. The word limit did more work than the bullet structure did.
- *What failed:* one real loss. Version 3's single-click hypothesis was its sharpest contribution and here it is compressed into a supporting bullet rather than flagged as something to test. Compression cost me the most interesting idea.
- *What next:* make it separate what it knows from what it is inferring.

---

## Version 5: verification requirement

**Layer added:** mark each claim as derived from the given numbers or inferred from outside knowledge, and name the check that would settle anything unresolved.

**Output (excerpt):** Every bullet tagged `[derived]` or `[inference]`. Exactly one inference: that 0.29% is orders below published position-1 CTR, so decile 0 is likely mid or long-tail positions. Supplied a groupby that would settle position range, volume confound and zero-inflation in one call.

**Notes**
- *What changed:* verification requirement.
- *What improved:* it isolated the one claim I should distrust. The single `[inference]` tag sits on external knowledge I cannot check from my data, which is the same shape of claim that went wrong in version 2. Now it is labelled instead of buried. It also handed me a runnable check rather than telling me to go and verify something.
- *What failed:* the tagging is self-reported, so it marks what it believes it derived. That is a claim about its own reasoning, not a guarantee.
- *What next:* nothing on this ladder. The next real improvement is running the check it gave me.

---

## Final reusable prompt
