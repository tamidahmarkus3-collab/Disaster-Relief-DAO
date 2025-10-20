# Disaster-Relief-DAO 🌐🚑

A minimal Disaster Relief DAO on Stacks. Members join, create funding proposals for recipients, vote, and execute approved disbursements from the contract treasury.

## Features
- Open membership with 1 vote weight per member
- Create proposals with recipient, amount, and memo
- Vote yes/no during a fixed voting window
- Quorum and simple majority required
- Disburse STX from contract to recipient on successful execution

## Contract
- Name: `disaster-relief-dao`
- File: `contracts/disaster-relief-dao.clar`
- Clarity: v3 (uses `stacks-block-height` and `get-stacks-block-info?`)

## Quickstart ⚡
1) Install Clarinet and run checks
```
pwsh
clarinet check
```

2) Normalize line endings (Windows) ⏎
Run for both files to ensure LF endings:
```
pwsh
(Get-Content "contracts/disaster-relief-dao.clar" -Raw).Replace("`r`n", "`n") | Set-Content "contracts/disaster-relief-dao.clar" -NoNewline
(Get-Content "README.md" -Raw).Replace("`r`n", "`n") | Set-Content "README.md" -NoNewline
```

3) Open console and interact 🧪
```
clarinet console
```
Examples in the REPL:
```
(contract-call? .disaster-relief-dao join)
(contract-call? .disaster-relief-dao propose 'SP3FBR2AGK8N9Z6N9G8M7XDRQK8Z5B9AFZ4C1REC1 u100000 "Flood Aid")
(contract-call? .disaster-relief-dao vote u1 true)
(contract-call? .disaster-relief-dao execute u1)
```

## Key Public Functions 🔑
- `join` -> become an active member
- `leave` -> deactivate membership
- `propose(recipient, amount, memo)` -> open a proposal
- `vote(id, support)` -> cast vote once per member
- `execute(id)` -> disburse if quorum and majority are met
- `cancel(id)` -> proposer can cancel before voting ends

## Read-only Helpers 🧭
- `get-member(principal)`
- `get-proposal(uint)`
- `list-proposal-stats(uint)`
- `get-total-weight`
- `get-current-height`
- `get-treasury`

## Notes
- Treasury is the contract’s STX balance. Fund it by sending STX directly to the contract principal from your wallet.
- Voting period is 144 blocks. Quorum is 20% of total active weight. Simple majority decides.
