## Adarsh Bhardwaj

I build AI systems for the two places a wrong answer costs you something real:
money and health.

One idea runs through all of it — **the model never produces a number.**
Tested code computes every figure; the model's job is to pick the right tool
and explain what came back. Then a verifier checks the answer against those
tool outputs and rejects anything it cannot trace. Prompting asks a model to
behave; this makes misbehaviour unable to reach a user.

---

### What I'm building

**[paisa-core](https://github.com/Adarsh-9182/paisa-core)** — an AI-native ERP
with an AI CFO on top. Perpetual double-entry ledger where balances are
projections over an append-only journal, ASC 606 revenue recognition, a close
that runs executable checks rather than tickable boxes, Indian GST, and a
Stripe connector that refuses non-INR charges rather than converting them at a
rate nobody supplied. 240 tests. → [askpaisaai.com](https://www.askpaisaai.com)

**[nutritiscan-ai](https://github.com/Adarsh-9182/nutritiscan-ai)** — an AI
health agent with a deterministic triage layer underneath the chat. It runs
*before* the model reasons, fails closed on error, and can end the turn. A
model may raise suspicion; nothing it says can lower a rule-derived verdict.

### Extracted and published

**[agent-framework](https://github.com/Adarsh-9182/agent-framework)** — the
grounding machinery from Paisa as a standalone library: a tool registry, an
orchestrator that records every call, and a verifier that rejects ungrounded
answers.

Writing it standalone paid for itself immediately. The first test found that
the original searched tool output as one string, so `₹26` counted as grounded
by a balance of `₹32,42,600` — a wrong number verifying as correct. The fix
went back into Paisa.

**[rag-financial-assistant](https://github.com/Adarsh-9182/rag-financial-assistant)**
— retrieval you can cite, for corpora where being unreproducible is
unacceptable. Deliberately not embeddings: for a curated corpus of hundreds of
passages, the same question returning the same passages — inspectable when a
result looks wrong, pinnable in CI — is worth more than the recall.

---

### How I work

I read code to find bugs rather than waiting for issues. Recent: a differential
harness across Keras's numpy/jax/torch backends surfaced eleven `keras.ops`
functions that handle integer inputs inconsistently — two of them silently
doing integer division, so `reciprocal([1,2,3,4])` returns `[1,0,0,0]` and
`1/0` returns `INT_MAX` instead of `inf`.

The failures I care most about are the quiet ones. A crash gets fixed. A wrong
number that looks right gets shipped.

**TypeScript · Node · Python · Next.js · Anthropic API · MCP · Postgres · Vitest**

[adarshbhardwaj.space](https://adarshbhardwaj.space) · [LinkedIn](https://www.linkedin.com/in/adarsh-bhardwaj-925b31263) · adarshbhardwaj9182@gmail.com
