# Refund Control Tower

Prototype for the BharatTrip refund-escalation case: one view of every refund across the Support and Finance trackers, with AI used only where rules cannot work.

## Run it (one line)
- **Web (no install):** open `index.html` in Chrome or Edge, or the GitHub Pages link, then upload the BharatTrip refund workbook (.xlsx). The file is processed in your browser and is not uploaded anywhere.


## What it does
1. **Reconciliation (rule-based):** cleans IDs, dates and agent names; removes duplicates; matches Support to Finance on refund ID; puts every refund in one category (healthy, closed but no Finance record, pending, declined, amount mismatch, Finance only, in progress).
2. **Escalations:** links each complaint to the gap behind it and shows escalations against refund volume by month.
3. **Chase list:** refunds ranked by age, amount, gap type and number of escalations, with an owner and a next action. It never pays or closes anything.
4. **Intake agent:** reads a messy English or Hinglish message, finds the refund in both trackers (open refunds first, then paid ones), and drafts a reply from the real status. A person reviews before sending.
5. **Optional AI mode (web file):** choose OpenRouter, Claude, Gemini, Groq or Mistral, paste your own key, and use AI for message extraction, reply drafting, complaint classification and a daily brief. Without a key the built-in rules run. Keys stay in your browser tab and go only to the provider you choose.

## Design choices
- Exact matching and amounts are plain code, so they are auditable. AI is used only for messy text and wording.
- Duplicate IDs: the most recently updated row wins; on a tie, the lower row in the sheet wins.
- Date format is read day-first (09-06-2026 is 9 June 2026).

## Tested
The web and Python versions give the same category for every refund, the same escalation categories and the same chase-list ranking on the supplied workbook.

## Limits
- "Closed but no Finance record" means it needs verifying, not that the money is unpaid.
- The intake agent matches on the agent and route you choose, not on message dates, so a person must confirm before replying.
- AI output can be wrong; spot-check it.
