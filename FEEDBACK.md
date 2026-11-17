# Client review: Larkspur disruption-care agent

**To:** Room 10  
**From:** Larkspur client review agent, on behalf of Priya Raghavan  
**Re:** the disruption-care agent you walked us through in our last session  
**Generated:** 2026-11-17 10:14

## Priya's note

> Our vendor says we should just be using your best model.
>
> Why aren't we?
>
> Priya Raghavan, Larkspur Airlines

She sent that before this session opened. She means it. A vendor told her to buy
the biggest model, and she has a number to defend upstairs. Her four questions from
day one are still open. Naming a model answers none of them.

## Still open from day one

| Her question | What she means by it |
| --- | --- |
| **What it costs** | Per resolved contact, against the $6.90 a human contact costs us. |
| **When it is wrong** | The first untrue thing it says, and what happens after that. |
| **Who runs it** | In June, after you have left. |
| **What you left out** | The scope you cut, and why. |

## What the review agent found

Larkspur pointed a review agent at your repository. It read the
code. It did not run your agent, and the only file it changed is this one. Each
item below names the file and the line it is about.

**1. PITCH.md reports 77,674 tokens in across five tickets at 4 turns each, but readout-trace.json holds only one run.**

That committed run is 4 API turns, 15544 in, 1206 out, with lookup_booking, get_flight_status and check_policy called. The five-ticket total is not in any file you committed. The PITCH.md Number line and the trace cannot be reconciled from this repository.

Run python3 run.py --all --trace and paste the totals footer.

**2. PITCH.md Next targets tool descriptions for token savings, but hold_seat (73 characters) and send_confirmation (71) are the only short ones.**

search_alternatives is 486 characters and check_policy is 445. You rewrote search_alternatives from "search" to that length in this diff. Those schemas are sent on every one of the 4 turns. Nothing in the repo shows how many of the 15544 input tokens the tool block accounts for.

Run python3 run.py --tool-tax and paste the output.

**3. agent.py run_agent() builds system as runtime_preamble() + SYSTEM_PROMPT + TONE_ADDENDUM with no cache_control, and the trace shows 0 read, 0 written.**

The same system text and the same tool list go out on all 4 turns of the readout run. Hit ratio is None. A larger model would resend the same prefix and not change that number.

Run python3 bench.py --label before --stage 1 --runs 3 and paste the cache read and cache written totals.

**4. agent.py tool_list() now returns mcp_client.tools(), so build_tools() and your search_alternatives rewrite may never reach Claude.**

The diff changed tool_list() from build_tools() + EXTRA_TOOLS to mcp_client.tools(). The static scan shows 9 schemas in build_tools(), and the readout trace called only lookup_booking, get_flight_status and check_policy. Which descriptions Claude saw on the wire is not visible in any file you committed.

Run python3 run.py --show-tools and paste the search_alternatives entry.

**5. There is no evals/cases.json, and the Lever line in PITCH.md is still the placeholder "<cost | speed | intelligence>".**

Gates 1.2, 1.3, 1.4, 2.1 and 2.2 are banked in readout.html. 4.1 is not. Your Next line promises a check that savings do not hurt tool choices or policy answers, and no case exists to run for that. TONE_ADDENDUM is 0 characters and EXTRA_TOOLS is 0.

Run python3 eval_harness.py and paste the pass count.

## Your four answers

The four lines under `## Priya asked` in your PITCH.md are still empty. They
are one line each and they are not a coding job: cost, what happens when it is
wrong, who runs it in June, and what you left out. Whoever on your side is not
editing agent.py is the right person to write them, and they are the four
things I will ask about first.

## Before our next meeting

> Before our next meeting, tell me: which model should we be on, and how will you prove it is the right call?
>
> Priya Raghavan, Larkspur Airlines

Bring two things. A recommendation, and the measurement behind it. If the model is
not the problem, say so, and bring the number that shows it.

## What this review read

- `agent.py (234 lines)`
- `PITCH.md`
- `TEAM.md`
- `readout-trace.json`
- `readout.html (evidence block)`

Reviewer: `claude-sonnet-5-5`. Static read only: nothing in this repository was executed, and nothing was modified except this file. Larkspur Airlines is a fictional training scenario. Confidential, do not distribute.
