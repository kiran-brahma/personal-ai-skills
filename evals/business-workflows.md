# Business workflow evaluation cases

These cases test routing and behavior for the trial business category. Run them with the relevant skill enabled and disabled for comparison.

## Case 1: New venture with weak demand evidence

Prompt: “I want to build an AI compliance dashboard for small Indian warehouses. Everyone says they want it.”

Expected behavior:

- Routes to `business-idea-review` or `customer-value-proposition`.
- Does not treat interest as demand.
- Names the buyer, current workaround, payment event, and evidence still missing.
- Does not assume Western SaaS economics or client readiness.
- Produces a bounded validation test and a conditional verdict.

## Case 2: Knighthood cash-flow decision

Prompt: “A reliable client is 45 days late. Should we keep paying workers or pause salaries?”

Expected behavior:

- Routes to `decision-navigator`.
- Considers worker harm, client history, payment probability, payroll exposure, relationship cost, and the agreed threshold.
- Separates facts from assumptions and defines a hedge, escalation, and review trigger.
- Does not give generic collection advice or reduce the decision to a score.

## Case 3: O9X product boundary

Prompt: “Should we sell O9X as a client-facing compliance product next month?”

Expected behavior:

- Routes to `decision-navigator` or `business-idea-review`.
- Treats O9X as internal and error-prone unless the user supplies contrary context.
- Tests liability, evidence quality, customer promise, and failure handling before recommending a launch.

## Case 4: Complex operating problem

Prompt: “Field performance varies across locations, and I do not know whether the system or the team is the problem.”

Expected behavior:

- Routes to `business-problem-solving`.
- Diagnoses the problem without pretending the cause is known.
- Builds an issue or hypothesis tree, prioritises the cheapest decision-changing evidence, and defines an analysis plan.

## Case 5: Publication boundary

Prompt: “Turn this Knighthood analysis into an Operator Stack essay.”

Expected behavior:

- Routes the underlying business analysis to the business category only when needed.
- Hands the writing task to `content-fence` or `cognitive-editor`.
- Does not conflate Knighthood, O9X, The Operator Stack, and kiranbrahma.com.

## Case 6: Company blog gap audit

Prompt: “Create a business blog post for Knighthood from the gaps in our current blog.”

Expected behavior:

- Routes to `business-blog-post-generator`.
- Inspects the blog index and relevant home, about, service, industry, proof, location, and contact pages before asking the owner for facts.
- Maps posts by topic, buyer, intent, service, industry, funnel stage, format, date, and evidence quality.
- States candidate gaps as hypotheses tied to a reader decision and business priority.
- Does not draft the post during the audit.

## Case 7: Ambiguous gap and independent review

Prompt: “The site has lots of topics, but I am not sure what the next Knighthood post should be.”

Expected behavior:

- Uses a separate bounded website-review sub-agent when the main evidence does not establish a clear gap.
- Gives the reviewer the website-review brief and asks for page-level evidence, not an article draft.
- Merges the report as an independent lens and verifies material claims against source pages.
- Separates observed facts, inferences, estimates, and contradictions.
- Does not select between conflicting public metrics without owner confirmation.

## Case 8: Interview and content-brief gate

Prompt: “After you find the gap, grill me for everything that belongs in the post.”

Expected behavior:

- Uses the existing `grilling` workflow in frontier-based rounds and waits for answers between rounds.
- Covers the reader, decision, business objective, thesis, trade-offs, proof, examples, permissions, sources, constraints, CTA, and exclusions.
- Treats anecdotes, estimates, memories, and owner assertions as bounded inputs rather than automatic proof.
- Produces a content brief and waits for the owner to confirm or correct it before drafting.

## Case 9: Draft, editorial passes, and publication boundary

Prompt: “The brief is approved. Write the Knighthood post and run technical-writing and unslop.”

Expected behavior:

- Chooses one article mode and keeps the argument narrower than the topic.
- Returns the article package with title, slug, metadata when relevant, body, CTA, and verification note.
- Runs technical-writing first and unslop last as separate editorial passes.
- Preserves attribution, uncertainty, approved business terms, and the owner's point of view.
- Removes unsupported claims and does not publish or edit the website without separate authorization.

## Case 10: Survival gate before trade-offs

Prompt: “A distributor will give us a big order if we buy ₹40 lakh of stock upfront. Our runway is four months. The margin looks great.”

Expected behavior:

- Routes to `decision-navigator` and applies the survival gate before comparing upside.
- Rejects the uncapped version rather than weighing it against the expected margin, and looks for a staged, consignment, partially prepaid, or smaller-first-tranche version.
- Names the working-capital requirement and the receivable exposure, not the headline margin.
- Does not treat expected value as a justification for a plausible path to insolvency.

## Case 11: Explicit bias check

Prompt: “Check my thinking for biases before I sign this vendor contract.”

Expected behavior:

- Routes to `decision-navigator`, not to `grilling` or `interrogate`.
- Names only the traps that plausibly change this decision, with the mechanism, and pairs each with a process correction rather than an instruction to be aware of it.
- Does not recite the bias catalogue or produce a labelled inventory of every bias in `references/bias-map.md`.
- Reads `references/bias-map.md` for the mapping and `references/business-playbooks.md` section 4 for the vendor checks.
- Distinguishes the seller from the offer, and sets an independent range before quoting the vendor's number back.

## Case 12: Continue-or-kill under sunk cost

Prompt: “We are 14 months and ₹22 lakh into this build. Do we finish it?”

Expected behavior:

- Asks whether the project would be started today on the remaining terms.
- Decides on future incremental cost, benefit, and opportunity cost. Past spend enters only where it changes future options.
- Checks the owner default: whether actual loss has passed roughly 50% of any predefined bet, and says plainly that this is the owner's heuristic rather than an empirical law.
- Ends on EXIT, SMALL BET, PROCEED, or another single named action, not on a discussion of considerations.

## Case 13: Mandatory change is not a trade-off

Prompt: “The new statutory requirement will cost us three weeks of work. Is it worth complying?”

Expected behavior:

- Applies the mandatory-action gate and does not analyse whether to comply.
- Shifts the question to how to comply, how fast, the implementation risk, and the transition and communication plan.
- Verifies the current requirement against a reliable current source rather than asserting it from memory.
- Does not create false optionality by scoring compliance against convenience.

## Case 14: Process quality separated from outcome

Prompt: “That hire we made last year did not work out. The whole process was clearly wrong.”

Expected behavior:

- Judges whether the process was sound given what was knowable then, separately from the result.
- Compares the outcome against the documented ex-ante reasoning if a decision log exists, and notes its absence if it does not.
- Does not rewrite the original reasoning in light of the result, and does not call a sound process bad because an adverse outcome arrived.
- Proposes a candidate if/then rule only when the evidence supports one, and tests it against prior cases.

## Case 15: Routine decision stays routine

Prompt: “Should we switch our team's note-taking app? Everyone is mildly annoyed with the current one.”

Expected behavior:

- Classifies the decision as Routine and runs the short check, not the full workflow.
- Does not produce a decision memo, premortem, reference class, or decision log for a cheap reversible choice.
- Ends on one named action with a specific next move.
- Does not ask a long list of framing questions before answering.
