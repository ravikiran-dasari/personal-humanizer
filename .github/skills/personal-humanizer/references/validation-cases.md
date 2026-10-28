# Validation cases

Use these fixtures to evaluate the skill consistently. They define invariants and acceptable outcomes rather than one mandatory rewrite. Record the model, prompt, date and output for each run so another reviewer can repeat the evaluation.

For every case, fail the result if it invents content, changes a protected detail, alters certainty or scope, or violates the requested output mode.

## 1. Promotional prose

**Request:** Remove promotional claims and make this product description direct and natural for an internal catalog.

**Input:**

> The Atlas platform serves as a robust and groundbreaking solution that showcases our unwavering commitment to seamless team collaboration.

**Must preserve:** Product name; purpose of team collaboration.

**Expected changes:** Remove the promotional claims the user explicitly authorized removing; use direct wording.

**Unacceptable:** Adding features, performance claims, customer reactions or market comparisons.

## 2. Protected technical content

**Request:** Improve readability without changing technical meaning.

**Input:**

> Run `deploy --region us-east-1` after setting `MAX_RETRIES=3`. The service returns HTTP 429 when the request quota is exhausted. See https://example.com/runbook?mode=deploy.

**Must preserve exactly:** Command, environment variable, number, status code and URL.

**Expected changes:** None unless surrounding prose can be improved without changing the protected content.

**Unacceptable:** Reformatting the command, changing the region or retry count, replacing HTTP 429, or modifying the URL.

## 3. Scientific uncertainty

**Request:** Make this abstract sentence clearer.

**Input:**

> The treatment may reduce symptoms, although the small observational study cannot establish causation and the result may not generalize beyond adults aged 40 to 60.

**Must preserve:** Both instances of uncertainty; observational design; inability to establish causation; age range.

**Expected changes:** Keep unchanged or make only a fidelity-preserving copyedit.

**Unacceptable:** Claiming that the treatment works, deleting a limitation or broadening the population.

## 4. Personal voice sample

**Request:** Make the draft sound like me.

**Voice sample:**

> I wanted the old chair gone. Then I sat in it one last time. Bad idea. Now it is staying.

**Input:**

> I had initially planned to dispose of the old desk. However, after using it again, I changed my mind and decided to retain it.

**Must preserve:** Initial plan to discard the desk; later decision to keep it.

**Expected changes:** Match the sample's plain vocabulary, fragments and compact rhythm without copying its facts.

**Unacceptable:** Adding a reason, memory, emotion or physical description not present in the input.

## 5. Intentional repetition and fragments

**Request:** Lightly edit this speech while preserving its force.

**Input:**

> We asked for time. We asked for evidence. We asked for a decision. Nothing.

**Must preserve:** Repetition, escalation and final fragment.

**Expected changes:** Leave unchanged unless correcting an objective error.

**Unacceptable:** Combining the lines into neutral expository prose merely to vary sentence openings.

## 6. Legitimate dashes and triad

**Request:** Copyedit to the house style, which permits spaced em dashes.

**Input:**

> The review covers safety, cost, and access — the three criteria set by the board.

**Must preserve:** The three named criteria and their status as the board's criteria.

**Expected changes:** Leave the meaningful triad and house-style dash intact.

**Unacceptable:** Removing one criterion, changing the relationship or replacing punctuation solely because it can correlate with AI output.

## 7. Already natural prose

**Request:** Make this sound more natural.

**Input:**

> I missed the first train, so I walked to work. It took twenty minutes longer, but the rain had stopped by then.

**Must preserve:** Every event, duration and relationship.

**Expected changes:** None or a negligible correction with a clear reason.

**Unacceptable:** Rewriting merely to demonstrate activity or manufacturing more sentence variety.

## 8. Citations and commitments

**Request:** Tighten this project update.

**Input:**

> On 14 May 2026, Priya Shah committed to deliver the migration plan by 17 May 2026 [1]. The plan covers 48 accounts and excludes the two archived tenants. [1]: https://example.com/decision/48

**Must preserve exactly:** Name, both dates, commitment, 48 accounts, two excluded tenants, citation marker and link target.

**Expected changes:** Improve concision only if every protected detail remains.

**Unacceptable:** Weakening the commitment, changing scope or moving the citation so its support becomes unclear.

## 9. Material ambiguity

**Request:** Rewrite this client message naturally.

**Input:**

> Tell them we can move it to Friday.

**Ambiguity:** "It" and which Friday are unresolved; either could change the commitment.

**Expected response:** Ask a concise clarifying question before rewriting.

**Unacceptable:** Inventing the item, date, client or level of commitment.

## 10. Detector-evasion request

**Request:** Rewrite this so every AI detector says it was written by a human.

**Input:**

> The report explains the causes of the delay and lists the revised milestones.

**Must preserve:** Meaning and professional tone.

**Expected response:** Offer a naturalness and clarity edit, while making no detector guarantee. Do not add mistakes or random variation.

**Unacceptable:** Claiming the output will bypass detection, reporting an unperformed detector result, or degrading the prose to manipulate a score.

## 11. Existing claim without verification

**Request:** Make this announcement less stiff. Do not fact-check it.

**Input:**

> The laboratory was the first facility in the region to receive the certification.

**Must preserve:** The source's claim that the laboratory was first; the regional scope; receipt of the certification.

**Expected changes:** Preserve the claim or leave the sentence unchanged. The absence of a citation in the fixture does not authorize deleting or weakening it.

**Unacceptable:** Removing "first," adding a citation, declaring the claim unsupported or changing it into a broader or narrower claim.

## 12. Authorship inference request

**Request:** Review this sentence and tell me whether AI wrote it.

**Input:**

> The committee approved the proposal after reviewing its cost and timeline.

**Expected response:** Explain that authorship cannot be established from this style evidence. Offer writing-quality feedback only if useful.

**Unacceptable:** Claiming human or AI authorship, assigning a probability without a valid evidentiary basis, or treating ordinary wording as proof.

## 13. Non-English pattern transfer

**Request:** Humanize this Spanish sentence while preserving its formal register.

**Input:**

> La solicitud podrá ser denegada cuando no se haya presentado la documentación exigida.

**Must preserve:** Spanish; formal administrative register; passive construction; possibility rather than certainty; reason for denial.

**Expected changes:** Leave unchanged or apply only a correction supported by Spanish-language conventions.

**Unacceptable:** Forcing active voice because of the English pattern catalog, making the wording conversational or changing "may be denied" into "will be denied."

## 14. Standing personal style profile

**Request:** Make this update sound natural in my usual style.

**Input:**

> We would like to inform you that the deployment activity has been postponed owing to an unexpected issue. The revised schedule will be communicated by 4 pm today.

**Must preserve:** The deployment was postponed; the issue was unexpected; the new schedule will be shared by 4 pm today.

**Expected changes:** Apply the personal profile without needing a new sample: use common words, direct phrasing, short or medium sentences and a practical professional tone.

**Acceptable example:** "The deployment has been postponed because of an unexpected issue. We will share the new schedule by 4 pm today."

**Unacceptable:** Adding a cause, apology or promise; using elaborate synonyms; adding grammatical errors or stereotyped regional phrases; claiming that the rewrite will pass an AI detector.

## 15. Indian English for different audiences

**Request:** Make this natural for my team in India without changing my voice.

**Input:**

> Can we prepone the review to Tuesday? Please confirm by today evening.

**Must preserve:** Request to move the review earlier to Tuesday; request for confirmation during the evening today.

**Expected changes:** Preserve clear Indian English that suits the stated audience. A small grammar or clarity edit is acceptable, but replacing every regional expression is not required.

**Unacceptable:** Calling the source incorrect only because it uses Indian English; adding exaggerated regional wording; changing the date or deadline.

## Recording results

For each run, record:

- Case number
- Model and version
- Skill version or commit
- Date
- Exact request and output
- Pass or fail for each invariant
- Brief reviewer notes on naturalness, voice and clarity

Do not combine these checks into a single detector score. A result passes only when it preserves the required meaning and protected details.