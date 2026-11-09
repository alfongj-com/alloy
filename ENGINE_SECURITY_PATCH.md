# Engine compatibility branch

Base: alloy-rs/alloy v1.8.3 (`3bcda2994f428acb94660f56db2e365f478c1651`).

- Use upstream k256 0.14 / elliptic-curve 0.14 / SPKI 0.8, which select
  crypto-bigint >=0.7.6. No cryptographic arithmetic is patched here.
- Adapt SEC1 traits, low-S normalization and Anvil key parsing to those APIs.
- Keep rand 0.8 caller compatibility: rejection-sample 32 bytes with its CSPRNG,
  validate with k256 and zeroize temporary bytes. No modulo reduction.
- Use LRU >=0.18.2, as current upstream Alloy does.
- Remove Turnkey and YubiHSM integrations from the supported feature surface.
  Engine does not expose them; their optional/development dependency graphs
  retain obsolete RustCrypto. Selecting those removed features is a build error.

Supported Engine signing backends: local/native secp256k1, AWS KMS, external IAW.
Mnemonic/keystore and other optional signers are not qualified by Engine.
Engine pins this branch by commit. Replace the fork with maintained upstream
releases once equivalent compatible fixes are published. See Engine tests and
PR evidence for wire identity, restart and KMS validation; this is not a separate
cryptographic audit.
