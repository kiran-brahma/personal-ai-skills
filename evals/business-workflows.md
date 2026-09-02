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

