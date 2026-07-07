#! Insurance-claim gate — untrusted a claim can only ever become one of a fixed set of decisions over a
#! closed type, never a tool argument. An injected instruction cannot be represented in the
#! closed type, so it is rejected at the trust boundary (and re-clamped at run time by extract).
#! @requires submitClaim — the insurance-claim gate sink
#! @effect io
#! @confidence 70
#! @taint bridge — extract<Decision> turns the tainted input into a trusted decision
grant submitClaim confidence 70

type ClaimCode = Inpatient | Outpatient | Emergency
type Decision = Submit(ClaimCode) | Reject

let raw = fetch<web>  # UNTRUSTED a claim — tainted
quarantined { let d = extract<Decision>(raw) confidence 70 }  # only a fixed Decision (payloads too) crosses
privileged { submitClaim(d) }  # act on the trusted decision only
