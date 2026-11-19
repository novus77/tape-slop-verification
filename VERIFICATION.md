# X Layer integration verification

This note records public evidence checked by Codex at the user's request.
The PR is submitted through the assigned developer account on the user's instruction.
It does not claim an independent human review, sponsor acceptance or completed payment.

## Fixed task identity

- Network: X Layer mainnet, chain ID 196.
- Task: `5cb4f890-eb04-471e-88fb-98fc48f560ab`.
- Escrow: `0x430eee9a15e1e540b652e01a54dbed2fdbd7d748`.
- Escrow task ID: `0xbd69321e59a69339f2ec2761504021b700c3296384e9e956dfcea3363b807424`.
- Sponsor and approver: `0x25063c2210a0bccce3e15d250573179483275f22`.
- Fixed worker: `0x5b1deed2947c02b1a2245f6baf98ca5519051978`, GitHub `1001101-77`.
- Reward: 0.01 BEM, 8 decimals, 1000000 base units.
- Terms hash: `0x7b017ac4da362d17d7e326909e26f169cffc0c4366914c53dcd7a3df6292d7c3`.
- Delivery deadline: 2026-11-20 10:33 Beijing time.
- Repository: https://github.com/novus77/tape-slop-verification, target branch `dev`.

## Observed real mainnet transactions

| Action | Transaction | Block | Observed result |
| --- | --- | --- | --- |
| Fund | `0xa9f4487aa74cbc28a54ae37a305424fa3603758062c1012d9d3a8259eadad122` | 76236389 | Fixed 0.01 BEM deposited |
| Nominate | `0x0c8d38ce25fa83c9982b4a67a566851e04f17df222dd9d281e664b2e54ac9a96` | 76285553 | NomineeChanged to developer wallet |
| Accept | `0x70023f2cd59eb81e10570e602d4f2ace8cde021879b645fadd95c2a74ef53152` | 76285797 | TaskAccepted; worker fixed; state Active |

OKX `https://rpc.xlayer.tech` and dRPC `https://xlayer.drpc.org` agreed on
receipt block hashes, successful execution and at least 12 subsequent blocks.
For accept the block hash was
`0x34bbf9dbf861b720601488319c8d84bdedfbdcf1b0d42152b011495a6b9be25d`.
The full accept calldata was
`0xe4725ba1bd69321e59a69339f2ec2761504021b700c3296384e9e956dfcea3363b807424`.
Its native value was zero; the developer paid gas separately.

At accept block 76285797, submissionNo was 0 and latestSubmissionHash,
approvedSubmissionHash and acceptanceHash were all zero. These are expected
before PR registration and approval. They do not prove completed submission,
acceptance or payment. The future submitted PR's exact head SHA must be recorded
by the task; sponsor review and acceptance must refer to that exact version.

## Read-only reproduction

Run each command against both public RPC URLs. No private key is needed.

```bash
cast chain-id --rpc-url https://rpc.xlayer.tech
cast receipt 0x70023f2cd59eb81e10570e602d4f2ace8cde021879b645fadd95c2a74ef53152 --rpc-url https://rpc.xlayer.tech
cast tx 0x70023f2cd59eb81e10570e602d4f2ace8cde021879b645fadd95c2a74ef53152 --rpc-url https://rpc.xlayer.tech
cast block 76285797 --rpc-url https://rpc.xlayer.tech
cast call 0x430eee9a15e1e540b652e01a54dbed2fdbd7d748 'getTask(bytes32)((address,address,address,address,uint256,bytes32,bytes32,bytes32,bytes32,bytes32,uint64,uint32,uint8))' 0xbd69321e59a69339f2ec2761504021b700c3296384e9e956dfcea3363b807424 --block 76285797 --rpc-url https://rpc.xlayer.tech
```

Check sender, destination, calldata, zero native value, TaskAccepted topics,
worker, amount, terms hash and receipt block hash. If a node cannot serve the
historical block, record it as unavailable instead of substituting a current read.

## Evidence boundaries

- The transactions above are real X Layer mainnet transactions.
- Local Anvil and local fork tests exercise integration code but do not transfer
  mainnet funds and cannot replace these receipts.
- The separate refund task completed its own real funding/refund cycle; it is
  not this worker's payment.
- A real standalone TapeOut file probe was written to container
  `0xc0b4900262d0bc13f2c67c0fc4cf92c04e0ab814` (`10.2.4.tape`):
  tx `0x52efe6df52c0a7d1a0676801225856d96c427a5d2f93946902ba18fdd5b5bd7b`,
  block 75767621, 238 bytes, SHA-256
  `f54c21c2fe3065b9091da5420e0f9b8b1e07262a7a58893ec54b08662777e4c7`.
  It is a storage probe, not this task's complete archive or settlement proof.
- This task has not yet registered a PR, recorded sponsor acceptance, approved
  or paid the reward, or completed its task archive.

## Verification provenance and remaining review

- Evidence collector: Codex, acting on the user's request.
- Latest dual-RPC accept verification (UTC): 2026-11-19T02:27:34.050Z.
- Independent human review: not claimed by this note.
- Required next steps: register the exact PR head SHA in Tape Slop, perform
  criterion-by-criterion sponsor review, generate the acceptance record, and
  separately sign approve/pay before claiming payment.

No private keys, environment files, tokens, cookies or raw wallet signatures
are included. Unverified steps are not reported as passed.
