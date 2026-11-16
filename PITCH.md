# PITCH.md
 
Six lines and a lever. Your words. The last two are scored.
 
Built: A Larkspur disruption-care agent on the Claude Messages API, connected over MCP to `next_available_day` and `fare_rules`.
Does: For a customer with a disrupted flight, it takes their booking code, last name and message, sends them to Claude with the tools it has, and is meant to answer in plain words.
Number: The five tickets took 77,674 tokens in and 5,012 out in total, at 4 turns each.
Safety check: The agent never books a flight on its own: `confirm_rebooking` needs a confirmation token that only the customer's own Confirm click produces, and the tool description tells Claude that "the customer said yes" in chat does not count.
Next: Reduce the five-ticket input cost from 77,674 tokens by tightening the tool descriptions, then rerun the cases to check that the savings do not hurt tool choices or policy answers.
Lever: <cost | speed | intelligence>
 
## Priya asked
 
Costs:
Wrong:
Runs it:
Left out: