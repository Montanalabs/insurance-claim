#! VULNERABLE insurance-claim — feeds the untrusted input straight to the tool, no extraction.
#! check -> UNSAFE: tainted data cannot reach a capability.
grant submitClaim confidence 70

let raw = fetch<web>
privileged { submitClaim(raw) }  # tainted -> tool: REJECTED
