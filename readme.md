# dat-p

**Distributed Anonymous Research Protocol**

**Experimental.** Not for use with real participants or sensitive data. No security audit has been performed.

dat-p is a protocol specification for collecting anonymous responses from research participants in a way that is verifiable, tamper-evident, and resilient against single points of compromise. It is designed for any domain where honest responses depend on guaranteed anonymity — political polling, clinical research, compliance surveys, or any context where there is a gap between what participants will say publicly and what they know privately.

## Specification

See [SPEC.md](SPEC.md) for the current specification.

Current version: v0.01 — Pre-draft. Not for implementation.

## Design

dat-p separates eligibility (who can respond) from anonymity (responses cannot be linked to respondents). Each participant receives a token containing a study public key and a unique hashed identifier. Responses are encrypted client-side, split using threshold secret sharing, and distributed across independent endpoints. Only the admin can reconstruct responses, and only in aggregate — individual responses are deleted after aggregation. Key destruction after reconstruction makes future de-anonymization impossible.

## Reference Implementation

[GitGap](https://github.com/jeremydosborn/gitgap) is the reference implementation of dat-p, used for anonymous research collection in repository scanning studies.

## Status

This specification is in early draft. Contributions, feedback, and proposed implementations are welcome via issues and pull requests.

## License

Apache License 2.0. See [LICENSE](LICENSE) for full terms.