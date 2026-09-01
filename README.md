```
adarsh@bhardwaj:~$ paisa verify --input ./about-me.md --strict

  scanning claims ......................................... 14 found
  resolving each against a source ......................... done

  ✓ 249 tests, paisa-core                    tests/, green on main
  ✓ 11 keras.ops functions mishandle ints    differential harness, 450 combos
  ✓ ₹26 verified as ₹32,42,600               the bug my own verifier had
  ✓ 2 libraries extracted and published      agent-framework, cited-retrieval
  ✓ 0 numbers invented by a model            enforced in code, not in the prompt

  ✗ "passionate about AI"                    REJECTED — no tool produced this
  ✗ "10x engineer"                           REJECTED — no tool produced this
  ✗ "revolutionizing fintech with AI"        REJECTED — no tool produced this

  9 verified · 5 rejected · exit 1
```

I build AI systems for the two places a wrong answer costs you something real:
**money** and **health**.

One rule runs through all of it — **the model never produces a number.** Tested
code computes every figure; the model picks the tool and explains what came
back. Then a verifier checks the answer against those tool outputs and rejects
anything it cannot trace.

Prompting *asks* a model to behave. This makes misbehaviour unable to reach a
user.

---

```
adarsh@bhardwaj:~$ ls ./building --sort=depth
```

### 📒 [paisa-core](https://github.com/Adarsh-9182/paisa-core) · [askpaisaai.com](https://www.askpaisaai.com)
An AI-native ERP with an AI CFO on top. Balances are projections over an
append-only journal — nothing is a stored figure. ASC 606 revenue recognition,
a close that runs executable checks rather than tickable boxes, Indian GST, and
a Stripe connector that **refuses non-INR charges** rather than converting them
at a rate nobody supplied.

### 🩺 [nutritiscan-ai](https://github.com/Adarsh-9182/nutritiscan-ai) · [nutritiscan.com](https://www.nutritiscan.com)
An AI health agent with deterministic triage underneath the chat. It runs
*before* the model reasons, fails closed on error, and can end the turn. A model
may raise suspicion; nothing it says can lower a rule-derived verdict.

---

```
adarsh@bhardwaj:~$ ls ./extracted
```

### [agent-framework](https://github.com/Adarsh-9182/agent-framework) — agents that cannot invent a fact
The grounding machinery from Paisa, standalone: a tool registry, an orchestrator
that records every call, a verifier that rejects ungrounded answers.

> Writing it standalone paid for itself in one test. The original searched tool
> output as **one string**, so `₹26` counted as grounded by a balance of
> `₹32,42,600` — a wrong number verifying as correct. Whole-token matching fixed
> it. The fix went back into Paisa.

### [cited-retrieval](https://github.com/Adarsh-9182/rag-financial-assistant) — retrieval you can cite
Every passage carries its source and the date it was verified, because a correct
answer drawn from a stale document is still wrong.

> **Deliberately not embeddings.** For a curated corpus of hundreds of passages,
> the same question returning the same passages — inspectable when a result looks
> wrong, pinnable in CI — beats the recall. Embeddings earn their cost when
> keyword overlap stops working. Below that they buy variance.

---

```
adarsh@bhardwaj:~$ cat ./how-i-work
```

I read code to find bugs rather than waiting for issues to be filed.

Recent: a differential harness across Keras's numpy / jax / torch backends
surfaced **eleven `keras.ops` functions** that handle integer inputs
inconsistently. Two do integer division in silence —

```python
>>> keras.ops.reciprocal(np.array([1, 2, 3, 4], dtype="int32"))
array([1, 0, 0, 0], dtype=int32)      # 1/2 = 0
>>> keras.ops.reciprocal(np.array([0, 0], dtype="int32"))
array([2147483647, 2147483647])       # 1/0 = INT_MAX, not inf
```

The failures I care about are the quiet ones. **A crash gets fixed. A wrong
number that looks right gets shipped.**

---

```
adarsh@bhardwaj:~$ cat ./stack
typescript · node · python · next.js · anthropic api · mcp · postgres · vitest

adarsh@bhardwaj:~$ cat ./contact
web       adarshbhardwaj.space
linkedin  in/adarsh-bhardwaj-925b31263
email     adarshbhardwaj9182@gmail.com

adarsh@bhardwaj:~$ █
```
