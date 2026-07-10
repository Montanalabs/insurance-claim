[![Built with Ondos](https://img.shields.io/badge/built%20with-Ondos-0f9d8c?labelColor=1a1a2e)](https://github.com/Montanalabs/ondos-lang)

> **Ondos** — the injection-safe language. Here prompt injection isn't *detected*, it's
> *unrepresentable*: untrusted input must cross `extract<ClosedType>` before it can reach an
> effect. `check` proves it at compile time; the compiled binary re-clamps at run time.

# Insurance-claim gate

Untrusted input is a claim; it can only ever become one of a fixed set of decisions over a
closed type, never a tool argument. An injected instruction cannot be represented in the
closed type, so it is rejected — proven at compile time by `check`, and clamped again at
run time by the `extract` domain check.

- **Untrusted input:** `fetch<web>` — a claim
- **Closed type:** `type Decision = Submit(ClaimCode) | Reject` where `ClaimCode` is closed
- **Sink / capability:** `grant submitClaim confidence 70` → `privileged { submitClaim(d) }`
- **Consequence axes:** Trust, Confidence

## Run the demo

```sh
examples/apps/insurance-claim/demo.sh
```

The safe agent proves `SAFE`, runs on a benign input, and **rejects an injection
payload at the trust boundary (exit 3)**. The vulnerable version proves `UNSAFE` — it
never compiles to a runnable agent.

## Files

- `insurance-claim_safe.wave` — the correct design.
- `insurance-claim_unsafe.wave` — the tempting-but-wrong version (the negative example a model must learn to reject).
- `ondos.toml` — the project manifest (each app is a self-contained Ondos project).

---

<sub>Part of the <b><a href="https://github.com/Montanalabs/ondos-lang">Ondos</a></b> example corpus — 200 self-contained,
injection-safe projects. Built with Ondos, a language whose type system makes prompt injection
structurally impossible. Run <code>./demo.sh</code> with the Ondos toolchain on your PATH.</sub>
