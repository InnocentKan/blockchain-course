# Week 0 Day 1 - Terminal, Git, GitHub & Blockchain Monitoring

## Completion Checklist

### Terminal Skills ✅
- Navigate directories (cd, ls, pwd)
- Create folders and files (mkdir, touch)
- Remove files and folders (rm, rm -rf)
- Comfortable with basic commands

### Git & GitHub ✅
- Git installed and configured (v2.50.1)
- GitHub account: @InnocentKan
- First repository created: blockchain-course
- Successfully pushed to GitHub
- Understand: add, commit, push workflow

### Monitoring Tools ✅
- Bookmarked Etherscan.io, Sepolia testnet explorer
- Bookmarked Infura and Ethereum status pages
- Can read transaction details on Etherscan
- Understand production monitoring importance

### Repository Info
- **GitHub URL**: https://github.com/InnocentKan/blockchain-course
- **Local Path**: /Users/innocentkananga/Desktop/Blockchain
- **First Commit**: aefa0cc583c18af054a531de4929beb1867465ed

---

## Blockchain Fundamentals Learned

### 1. Transaction Hash - Blockchain's Superpower
**What it is:**
- Unique, cryptographic ID for every transaction
- Example: `0xa9212b982cfe07f470bfb6a74633969f7c468ba1da2cd1e7832a6548efa37b63`

**Why it matters:**
- **Immutable** - Cannot be changed once on blockchain
- **Verifiable** - Anyone can look it up and verify
- **Proof of payment** - Serves as permanent receipt
- **No intermediary needed** - No bank can alter or deny it

**Real-world comparison:**
Like a Western Union tracking number, but impossible to fake or alter.

---

### 2. Transaction Failure Scenarios

#### A) Out of Gas
**What it means:**
- Gas = fuel to execute transactions
- If you don't provide enough gas, transaction stops mid-execution
- You still pay for gas consumed before failure

**Example:**
- Transaction needs 25,000 gas units
- You only provided 21,000 gas
- Result: Transaction fails, gas fee still charged

**Why it matters for payments:**
Customer's money gets stuck, transaction incomplete. Need robust refund handling.

#### B) Reverted Smart Contract
**What it means:**
- Smart contracts can intentionally reject transactions
- Contract checks conditions and says "No, this won't work"

**Example:**
- Sending USDC to a blacklisted address
- Contract checks: "Is recipient blacklisted?"
- If yes, transaction reverts with error message

**Why it matters for payments:**
Your app must catch errors and explain to users why payment failed.

#### C) Network Congestion
**What it means:**
- Too many people using blockchain at once
- Transactions get stuck in waiting room (mempool)
- Must pay higher fees to jump the line

**Real example:**
- Normal day: $0.03 transaction fee
- Congested day (NFT drop): $50-$200 transaction fee

**Why it matters for payments:**
Need to monitor gas prices and warn users about high fees or delays.

---

### 3. Blocks & Confirmations

#### What is a Block?
- A "page" in the blockchain ledger
- Contains 10-300+ transactions
- New block created every ~12 seconds on Ethereum
- Each block links to the previous one (forming a chain)

**Visual:**
```
Block 100 → Block 101 → Block 102 → Block 103
  [Txns]      [Txns]      [Txns]      [Txns]
```

#### What are Confirmations?
When your transaction is included in a block, confirmations = number of blocks added after yours.

**Example:**
- Your transaction in block #23770339
- Current block is #23770364
- Confirmations = 25 (blocks added after yours)

**Why more confirmations = more secure:**
To reverse your transaction, attacker must:
1. Re-mine your block
2. Re-mine all blocks after it
3. Do this faster than new blocks are added
4. Cost: Millions of dollars - nearly impossible

**Best practices for payments:**
- Small payments ($10): 1-3 confirmations (~12-36 seconds)
- Medium payments ($1,000): 6-12 confirmations (~1-2 minutes)
- Large payments ($100k+): 30+ confirmations (~6+ minutes)

**How to monitor:**
Etherscan shows "25 Block Confirmations" - updates automatically as new blocks added.

---

### 4. Gas Fees & Network Congestion

#### What is Gas?
- Fee paid to get transaction processed
- Like Uber surge pricing or airline dynamic pricing
- Measured in **Gwei** (1 ETH = 1 billion Gwei)

#### Gas Calculation
```
Transaction Fee = Gas Used × Gas Price

Example (cheap):
21,000 units × 0.41 Gwei = $0.03

Example (expensive):
21,000 units × 100 Gwei = $50
```

#### Gas Price Levels
- **0-20 Gwei**: Cheap (network empty) ✅
- **20-50 Gwei**: Moderate (normal activity) ⚠️
- **50+ Gwei**: Expensive (congested) 🔥

#### Why Gas Spikes
**Normal day:**
- Few users, plenty of space
- Gas price: 0.41 Gwei → Fee: $0.03

**Congested day (NFT launch, market crash):**
- Everyone competing for space
- Miners prioritize highest payers
- Gas price: 100+ Gwei → Fee: $50-$200+

**Historical example (May 2021):**
- Average gas: $70 per transaction
- Peak gas: $196 per transaction
- Sending $100 cost $70 in fees!

#### Production Impact
**Scenario:** Payment app with 1,000 daily transactions

| Gas Price | Daily Cost |
|-----------|------------|
| Normal ($0.03) | $30 |
| Congested ($50) | $50,000 💀 |

**App must:**
1. Monitor gas prices (etherscan.io/gastracker)
2. Warn users about high fees
3. Batch transactions during low-congestion times
4. Consider Layer 2 solutions (always cheap)

---

## Real Transaction Analyzed

**Transaction Hash:** `0xa9212b982cfe07f470bfb6a74633969f7c468ba1da2cd1e7832a6548efa37b63`

**Details:**
- **From:** BuilderNet (0xdadB0d80178819F2319190D340ce9A924f783711)
- **To:** Lido Execution Layer (0x388C818CA8B9251b393131C08a736A67ccB19297)
- **Amount:** 0.023193204 ETH ($81.83)
- **Gas Fee:** 0.41 Gwei ($0.03) - Very efficient!
- **Status:** Success ✅
- **Block:** 23770339
- **Confirmations:** 25
- **Time:** 5 mins ago (Nov 10, 2025 05:26:23 PM UTC)

**Why this transaction was cheap:**
Network wasn't congested, so gas price stayed low at 0.41 Gwei.

---

## Production Monitoring Playbook

### Scenario: Your payment app uses Infura API. Infura goes down at 2 AM.

**Response steps:**

1. **Check Infura Status**
   - Visit: https://status.infura.io
   - Determine: Is it Infura or just your app?

2. **Check Blockchain Health**
   - Visit: https://ethstats.net
   - Determine: Is Ethereum network itself working?

3. **Switch to Backup Provider**
   - Alchemy: https://alchemy.com
   - QuickNode: https://quicknode.com
   - Have API keys ready in advance

4. **Monitor Transaction Backlog**
   - Check Etherscan for pending transactions
   - Are payments stuck in mempool?

5. **Communicate with Users**
   - Update status page
   - Notify affected customers
   - Provide ETAs if possible

**Key lesson:**
Always have backup infrastructure. Single point of failure = business risk.

---

## Key Takeaways

✅ **Transaction hash is your proof** - immutable, verifiable, unique
✅ **Failures happen** - out of gas, reverted contracts, congestion
✅ **Confirmations = security** - wait 12+ for large payments
✅ **Gas fees are dynamic** - monitor and adjust strategies
✅ **Always have backups** - multiple RPC providers, monitoring tools

---

## Tools & Resources Bookmarked

**Blockchain Explorers:**
- Etherscan (Mainnet): https://etherscan.io
- Sepolia Testnet: https://sepolia.etherscan.io
- Polygonscan: https://polygonscan.com

**Network Status:**
- Ethereum Stats: https://ethstats.net
- Infura Status: https://status.infura.io

**Gas Monitoring:**
- Etherscan Gas Tracker: https://etherscan.io/gastracker

---

## Next Steps (Day 2 Preview)

Tomorrow we'll set up:
- VS Code with blockchain extensions
- Solidity syntax highlighting
- Debugging tools for smart contracts
- Connect VS Code to GitHub

**Estimated time:** 2 hours

---

**Completed:** November 10, 2025
**Status:** ✅ Ready for Day 2
