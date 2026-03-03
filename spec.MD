# dat-p: Distributed Anonymous Testimony Protocol
### Specification v0.5

**Status:** Experimental.
**License:** Apache 2.0. No warranties expressed or implied.

---

## What it is

dat-p is a protocol for collecting anonymous responses from research participants. It is designed for any domain where honest responses depend on guaranteed anonymity — political polling, clinical research, compliance surveys, academic research, or any context where there is a barrier between what participants will say publicly and what they know privately.

---

## How it works

**1. Setup**
The admin generates an asymmetric keypair per study. Each eligible participant receives a token containing the public key and a unique random identifier. The unique identifier is generated from a high-entropy random source, hashed with a per-study salt at generation time. Only the hashed identifier is distributed in the token and stored server-side. The plaintext identifier is never retained. No mapping between participant identity and token is retained after distribution. 

**2. Submission**
The participant's client uses the token to encrypt their response and split it into shares using threshold secret sharing (e.g. Shamir 2-of-3). One share goes to each independent endpoint alongside the unique identifier for deduplication. The unique identifier is hashed and carries no identifying information. The response payload is fully encrypted.

**3. Collection**
Independent endpoints store opaque shares. Endpoints know nothing about submission content or identity. Rate limiting prevents flooding.

**4. Reconstruction**
The admin collects threshold shares, reconstructs, decrypts with the private key, deduplicates by unique identifier, and aggregates responses. Individual responses are deleted after aggregation.

**5. Teardown**
The private key is destroyed. Future decryption becomes impossible. Share records at endpoints are deleted.

---

## Security properties

- Single endpoint compromise reveals nothing (shares below threshold are meaningless)
- Responses cannot be linked to participants by design
- Fixed-size padding prevents traffic analysis
- Key destruction after reconstruction provides a hard guarantee against future de-anonymization

---

## What this protocol does not cover

- Token distribution mechanism (left to implementer)
- Specific encryption scheme (any IND-CCA2 scheme is acceptable)
- Specific secret sharing scheme (any information-theoretically secure threshold scheme is theoretically acceptable)
- Endpoint infrastructure and hosting

---

## Status and versioning

This is a high level first draft. 

---

## License

Apache License 2.0. See LICENSE for full terms.