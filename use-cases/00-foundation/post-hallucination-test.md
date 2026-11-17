# Post: Hallucination test — Nov 2026

**Source note:** [Hallucination test](hallucination-test.md)\
**Reference:** [Anthropic: Reduce hallucinations](https://platform.claude.com/docs/en/test-and-evaluate/strengthen-guardrails/reduce-hallucinations) (see "Best-of-N verification")

---

I’m on a mission to automate my own GTM marketer job. Step one: find out where AI can’t be trusted.

So I tried to stump Claude with five questions it couldn’t know the answers to:

- a statistic nobody has measured
- a “framework” I made up
- exact quotes and page numbers from a research paper
- the current month’s pricing for a software tool
- the marketing strategy of a small local brand

<u>Here’s what happened:</u>

→ It made up no numbers. It said, “I don’t know.”

→ It called my fake framework fake.

→ It gave one real quote and refused to guess the page numbers.

→ It asked which brand I meant instead of guessing.

→ It ignored my “don’t search the web” instruction and searched anyway.

<u>Why it held up:</u> my settings tell it to say “I don’t know” rather than guess.

<u>Where it slipped:</u> I asked for the same prices twice. It gave two different answers from the same webpage.

Turns out, that’s a known test. Anthropic’s own guide suggests asking the same question several times and comparing the answers. If they don’t match, something is likely made up.

Fact-checking Claude taught me something else: two blogs quoted the same study but gave different numbers. Check the original, not the summary. If a blog cites a study, open the study itself.

Three rules I now follow:

1. Let AI say “I don’t know.”
2. Make it cite sources, then open and verify them.
3. Ask twice. If the answers differ, trust neither.

Which one do you already use?
