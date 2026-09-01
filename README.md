```
adarsh@bhardwaj:~$ whoami
```

I build AI systems for the two places a wrong answer costs something real:
money and health.

One rule runs through all of it — **the model never produces a number.** Tested
code computes every figure. The model picks the tool and explains what came
back. A verifier then checks the answer against those tool outputs and rejects
anything it cannot trace.

Prompting *asks* a model to behave. This makes misbehaviour unable to reach a
user.

---

**[paisa-core](https://github.com/Adarsh-9182/paisa-core)** · [askpaisaai.com](https://www.askpaisaai.com)
An AI-native ERP with an AI CFO on top. Balances are projections over an
append-only journal, not stored figures. ASC 606 revenue recognition, a close
that runs executable checks, Indian GST, and a Stripe connector that refuses
non-INR charges rather than converting them at a rate nobody supplied.
249 tests.

**[nutritiscan-ai](https://github.com/Adarsh-9182/nutritiscan-ai)** · [nutritiscan.com](https://www.nutritiscan.com)
An AI health agent with deterministic triage underneath the chat. It runs before
the model reasons, fails closed on error, and can end the turn. A model may
raise suspicion; nothing it says can lower a rule-derived verdict.

**[agent-framework](https://github.com/Adarsh-9182/agent-framework)**
The grounding machinery from Paisa, standalone — tool registry, an orchestrator
that records every call, and the verifier. 22 tests.

**[cited-retrieval](https://github.com/Adarsh-9182/rag-financial-assistant)**
Retrieval where every passage carries its source and the date it was verified.
Deliberately not embeddings: for a curated corpus, the same question returning
the same passages beats the recall. 12 tests.

---

```
adarsh@bhardwaj:~$ cat ./how-i-work
```

I read code to find bugs rather than waiting for issues to be filed.

Extracting the verifier into its own library found a bug in the original: it
searched tool output as one string, so `₹26` counted as grounded by a balance of
`₹32,42,600` — a wrong number verifying as correct. Whole-token matching fixed
it, and the fix went back into Paisa.

A differential harness across Keras's numpy, jax and torch backends found
`keras.ops` functions that handle integer inputs inconsistently. Two do integer
division in silence:

```python
>>> keras.ops.reciprocal(np.array([1, 2, 3, 4], dtype="int32"))
array([1, 0, 0, 0], dtype=int32)      # 1/2 = 0
>>> keras.ops.reciprocal(np.array([0, 0], dtype="int32"))
array([2147483647, 2147483647])       # 1/0 = INT_MAX, not inf
```

The failures I care about are the quiet ones. A crash gets fixed. A wrong number
that looks right gets shipped.

---

```
typescript · node · python · next.js · anthropic api · mcp · postgres · vitest

adarshbhardwaj.space
linkedin.com/in/adarsh-bhardwaj-925b31263
adarshbhardwaj9182@gmail.com
```
