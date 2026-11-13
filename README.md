# Tape Slop Integration Verification

Independent acceptance workspace for Tape Slop on X Layer (chain 196).
This repository records reproducible integration evidence. It is not a request
to modify an unrelated ecosystem project.

## Payment task — 0.01 BEM

The assigned developer submits a pull request containing a verification note:

1. Read the deployed BountyEscrowV1 contract on chain 196.
2. Confirm the fixed worker, reward, submission and acceptance identities.
3. Record public transaction hashes and observed block numbers from the task.
4. Describe which checks used real RPC, local Anvil, or a local fork.

The sponsor reviews the exact submitted commit against these criteria. A real
acceptance and on-chain approval are required before payment. A test label does
not authorize inventing a submission, review or wallet signature.

## Refund task — 0.01 BEM

This separate task tests an unassigned Open escrow deposit and refund. Nobody
is assigned to deliver it. After funding, the sponsor requests refund and
records the receipt and exact balance changes. It must not cancel an Awarded
obligation or consume a developer's accepted assignment.

## Evidence rules

- Never commit private keys, mnemonic phrases, OAuth tokens, session cookies,
  raw wallet signatures, RPC credentials or local environment files.
- Public addresses, contract calls, transaction hashes and file hashes are
  sufficient for this workspace.
- A local fork transaction is not a mainnet transaction.
- A successful allowance approval is not a funded bounty or a payment.
- A standalone TapeOut storage probe is not a complete task archive.
