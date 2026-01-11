#  CryptoVentures DAO – Governance System

CryptoVentures DAO is a **decentralized investment fund governance system** that enables token (stake) holders to collectively manage treasury allocations and investment decisions in a secure, transparent, and scalable way.

This project implements **production-grade DAO governance patterns** inspired by protocols like Compound, Aave, and MakerDAO, including weighted voting, delegation, timelocks, role-based execution, and multi-tier treasury management.

---

##  Key Features

###  Governance & Voting
- Stake-based governance using ETH deposits
- **Anti-whale voting power** (square-root weighted)
- Vote types: **For / Against / Abstain**
- One vote per member per proposal (immutable once cast)
- Delegated voting with **revocation support**
- On-chain readable voting power without voting

###  Proposal System
- Unique proposal IDs
- Proposal lifecycle:
**ending → Active → Queued → Executed / Defeated**
  - Proposal categories:
- **High Conviction** (large investments)
- **Experimental** (medium risk)
- **Operational** (small expenses)
- Category-based quorum, approval thresholds, and timelocks
- Spam prevention via minimum stake requirement

### Security & Execution
- **Timelocked execution** for approved proposals
- Configurable delays based on proposal risk
- Protection against double execution
- Graceful failure on insufficient treasury funds
- Emergency role-based execution control

### Treasury
- Segregated fund buckets per proposal category
- Role-restricted fund transfers
- Transparent balance tracking
- Event emission for all fund movements

###  Access Control
- Role-based permissions using OpenZeppelin AccessControl
- Roles supported:
- Proposer
- Voter
- Executor
- Guardian
- Clear separation of powers

---

##  Architecture Overview
CryptoVentures DAO follows a modular architecture with clear separation
between governance logic, treasury management, and access control.
Governance handles proposals, voting, delegation, and timelocks, while
the Treasury contract securely manages DAO funds with role-based execution.

---

## Project Structure

contracts/
├── access/
│ └── Roles.sol
├── treasury/
│ └── Treasury.sol
├── governance/
│ ├── Governance.sol
│ ├── Delegation.sol
│ ├── VotingPower.sol
│ └── ProposalTypes.sol
scripts/
├── deploy.ts
├── seed.ts
test/
├── 01.roles.test.ts
├── 02.treasury.test.ts
├── 03.staking-votingpower.test.ts
├── 04.proposal-lifecycle.test.ts
├── 05.delegation.test.ts
├── 06.timelock-execution.test.ts

---

##  Setup Instructions
### Install Dependencies
npm install

### Environment Variables
Create a .env file using .env.example:
cp .env.example .env

## Run Locally (One-Command Flow)
### Start Local Blockchain
npx hardhat node

### Deploy Contracts
npx hardhat run scripts/deploy.ts --network localhost

### Seed DAO State
npx hardhat run scripts/seed.ts --network localhost

### Run Tests
npx hardhat test
All governance, voting, delegation, timelock, and treasury tests pass successfully.

---

## Design Decisions & Trade-offs
### Anti-Whale Voting
- Square-root weighting prevents dominance by large holders
- Preserves fairness while still rewarding higher stake

### Timelock Enforcement
- Prevents rushed execution of high-risk proposals
- Allows time for review and emergency intervention

### Category-Based Governance
- Different risk levels demand different approval standards
- Enables faster operational decisions without compromising safety

### Modular Architecture
- Clear separation of governance, treasury, and access control
- Easier auditing, testing, and future upgrades

### Security Considerations

- Role-restricted execution
- Timelocked proposal execution
- Graceful failure on low treasury balance
- No hardcoded private keys
- Extensive test coverage for edge cases

### Evaluation Checklist
- Public GitHub repository
- One-command deployment
- One-command seeding
- One-command test execution
- Full governance lifecycle implemented
- Anti-whale voting & delegation
- Timelock & treasury controls
- Clean architecture & documentation

---

### Summary:
This project demonstrates a real-world DAO governance system, combining strong security practices, scalable governance design, and production-ready smart contracts. It is suitable for DeFi protocol governance roles, final-year projects, and portfolio showcase.
