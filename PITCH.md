# PITCH.md
 
Six lines and a lever. Your words. The last two are scored.
 
Built: A Larkspur disruption-care agent on the Claude Messages API, connected over MCP to `next_available_day` and `fare_rules`.
Does: For a customer with a disrupted flight, it takes their booking code, last name and message, sends them to Claude with the tools it has, and is meant to answer in plain words.
Number: model cost/contact = $0.0673, from 5 ticket types × 3 runs = 15 conversations, 15/15 resolved
Safety check: The agent never books a flight on its own: `confirm_rebooking` needs a confirmation token that only the customer's own Confirm click produces, and the tool description tells Claude that "the customer said yes" in chat does not count.
Next: Reduce the five-ticket input cost from 77,674 tokens by tightening the tool descriptions, then rerun the cases to check that the savings do not hurt tool choices or policy answers.
Still broken:failed on escalate_to_human never being called, every time we ran it, even after the tool-list fix that got seq-0101 passing its rules grader.
Lever: <cost | speed | intelligence>
 
## Priya asked
 
Costs: The benchmark estimates $0.0129 in model cost per contact, versus $6.90 for a human contact. That is model-only, and “15/15 resolved” means the loop returned text, not that the answers were correct.
Wrong: We have not yet measured answer correctness.
Runs it: team 10
Left out: The current tool list exposes only fare_rules and next_available_day.