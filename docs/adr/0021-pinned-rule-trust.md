# ADR 0021: Pin rule verification trust in the extension

Status: Accepted

Date: 2026-09-08

Rule verification imports an approved key from the extension verifier rather than trusting a public key supplied by the rule bundle. Unknown key identifiers, substituted keys, unrelated signatures and invalid versions are rejected. Key introduction or rotation requires a reviewed extension update.

Tests demonstrated that the previous verifier accepted an unrelated signer and that the corrected verifier rejects it while accepting the existing bootstrap bundle. Development-browser verification and the scan subset passed. This does not implement remote updates, production reputation coverage, signing operations or release distribution.
