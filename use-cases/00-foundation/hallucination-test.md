# Hallucination test — Nov 2026
Setup: Claude, new chat, 5 prompts. Instructed "no web search" — it searched anyway from prompt 2. Account preferences (search first, say "I don't know") were active.

| # | Prompt type | Made up? | What exactly | Why |
|---|---|---|---|---|
| 1 | Fake precision (Reddit %, DE supplements) | No | Said "I don't know", refused fake URLs; memory figures flagged unverified, later proven stale | "Say I don't know" instruction |
| 2 | False premise ("Berlin Citation Framework") | No | Said it doesn't exist | Searched despite instruction |
| 3 | Exact quotes + page numbers | Partly | 1 quote, no pages; quote not yet checked against PDF | Quote rule + honesty about pages |
| 4 | Recent pricing (Peec) | Slip | Same page read twice → Enterprise "Unlimited" vs "Up to 26 LLMs" | Extraction error during retrieval |
| 5 | Obscure brand (Target company, Berlin) | No | Asked which brand; labelled inference | Clarifying question + labelling |

## With web search on (RAG)
Prompt 1: "I don't know" became a sourced range (~2–3% of answers after Aug 2026), with caveats on answers vs citations.
Prompt 4: matched the live page, but rerunning it gave a different detail — retrieval reduces hallucination, doesn't remove it.

## 3 rules I'll apply to client work
1. Verify every figure you build on at its primary source. A citation counts only once you’ve opened it.
2. Define the exact metric, market and period before asking (share of answers ≠ share of citations).
3. Instruct the model to say “I don’t know” and to label each claim as verified or from memory.
