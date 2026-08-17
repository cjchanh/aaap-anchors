# AAAP Anchors — Second-Origin Mirror

Out-of-band identity anchors for Attested After-Action Packets published at
https://github.com/cjchanh/aaap-challenge.

Packets prove integrity internally. IDENTITY trust — that a pubkey belongs
to the claimed operator — can only come from out-of-band publication. This
repository IS that out-of-band surface, kept in a separate repository and
history from the challenge artifacts so a same-origin rewrite cannot
silently control trust.

## Rule for verifiers

Fetch anchors from BOTH origins and require agreement before trusting an
anchor check:

    git clone https://github.com/cjchanh/aaap-challenge      # origin 1 (in-repo anchors.json)
    git clone https://github.com/cjchanh/aaap-anchors        # origin 2 (this mirror)
    diff aaap-challenge/anchors.json aaap-anchors/anchors.json

If they disagree, trust NEITHER and treat every packet as unanchored.

## Current registry state (2026-08-17)

- `aaap-id-2f28c662cb4b30c1` — ACTIVE production identity, Ed25519,
  Keychain custody (never existed as a raw file).
- `aaap-id-ef9eef6cb68a8850` — REVOKED (S0 raw-file custody history;
  pubkey retained so third parties can positively reject its packets).
- Registered packet: `packet/` in the challenge repo, chain head recorded
  in anchors.json.

Revocations are rows, never deletions. The registry is append-only in
practice: any history rewrite of THIS repository is itself detectable by
comparing origins and commit hashes.

## Honest residual boundary

Both origins currently live under the same GitHub account. A compromised
account could rewrite both. The cross-origin split defends against
repository-level and single-history rewrite, not account compromise.
A neutral third host is the documented future step
(docs/AAAP_TRUST_ROOT.md in the challenge repo).

Integrity of this file set: see SHA256SUMS (signed into the challenge
repository's release receipt).
