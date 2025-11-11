# Week 0 Day 2 - VS Code + Blockchain Development Environment

## What We Accomplished Today

Today we set up a professional code editor (VS Code) configured specifically for blockchain development. This is the same setup used by developers at Coinbase, Stripe, Circle, and every major blockchain company.

**Key Achievement:** Transformed VS Code into a blockchain development powerhouse with syntax highlighting, debugging tools, and Git integration.

---

## Part 1: VS Code Installation

### What is VS Code?

Visual Studio Code (VS Code) is a free, powerful code editor created by Microsoft. It's the most popular editor among blockchain developers because:

- **Lightweight** - Opens fast, doesn't slow down your computer
- **Extensible** - Can add blockchain-specific tools via extensions
- **Integrated Terminal** - Write code and run commands in one window
- **Git Built-in** - Commit and push without leaving the editor

### Installation Process:

1. Downloaded from: https://code.visualstudio.com
2. Installed to Applications folder
3. Opened the Blockchain folder in VS Code using: `code .`

### VS Code Interface Overview:

```
┌─────────────────────────────────────────────────┐
│ Menu Bar (File, Edit, View...)                  │
├──────┬──────────────────────────────────────────┤
│      │                                           │
│ Side │          Editor                           │
│ Bar  │      (Where you write code)               │
│      │                                           │
│      │                                           │
├──────┴──────────────────────────────────────────┤
│          Terminal (Bottom)                       │
└─────────────────────────────────────────────────┘
```

**Why this matters for blockchain:**
When debugging a failed transaction at 2 AM, you need an editor that helps you spot errors quickly and access logs without switching windows.

---

## Part 2: Blockchain Extensions Installed

### What are Extensions?

Extensions add specialized features to VS Code. Think of them like apps on your phone - the base VS Code is the phone, extensions are the apps that make it powerful.

### Extensions We Installed:

#### 1. Solidity (by Juan Blanco)

**What it does:**

- Adds syntax highlighting for Solidity (the language for Ethereum smart contracts)
- Shows errors before you deploy (saves gas fees!)
- Auto-completes code (type `func` and it suggests `function`)

**Why you need it:**
Without this, Solidity code looks like plain text. With it, keywords are colored, making bugs easier to spot.

**Example:**

```solidity
// Without extension: all same color
contract Token { uint balance; }

// With extension: 'contract', 'uint' are colored differently
contract Token { uint balance; }
```

#### 2. Hardhat Solidity (by Nomic Foundation)

**What it does:**

- Integrates with Hardhat (testing framework we'll use later)
- Provides advanced Solidity features
- Links to documentation when you hover over keywords

**Why you need it:**
Professional smart contract development requires testing. This extension connects VS Code to Hardhat's testing suite.

#### 3. Prettier - Code Formatter

**What it does:**

- Auto-formats your code to look professional
- Fixes indentation, spacing, line breaks
- Enforces consistent style (tabs vs spaces, quotes, etc.)

**Why you need it:**
When reviewing code on GitHub or in pull requests, messy formatting makes bugs hard to spot. Prettier ensures your code always looks clean.

**Before Prettier:**

```javascript
const x = 1;
function test() {
  return x;
}
```

**After Prettier:**

```javascript
const x = 1;
function test() {
  return x;
}
```

#### 4. GitLens

**What it does:**

- Shows who changed each line of code and when
- Displays commit history inline
- Helps track down when bugs were introduced

**Why you need it:**
In team projects, you need to know who wrote problematic code. In solo projects, you need to remember why you made certain decisions.

#### 5. Error Lens

**What it does:**

- Displays error messages directly in the code (not hidden in a panel)
- Highlights problematic lines immediately
- Shows warnings inline

**Why you need it:**
When deploying a smart contract, one typo can cost thousands in gas fees or create security vulnerabilities. Error Lens catches mistakes before they're expensive.

#### 6. Python (by Microsoft)

**What it does:**

- Runs Python code
- Debugs Python scripts
- Autocompletes Python syntax

**Why you need it:**
Day 3 focuses on Python for API calls to blockchain networks. This extension makes Python development smooth.

#### 7. JavaScript (ES6) code snippets

**What it does:**

- Provides shortcuts for common JavaScript patterns
- Autocompletes async/await syntax
- Speeds up frontend development

**Why you need it:**
Day 4 covers JavaScript for payment interfaces. This extension makes JavaScript coding faster.

---

## Part 3: VS Code Settings Configuration

### Settings We Configured:

#### 1. Format on Save

**Setting:** `Editor: Format On Save` → Enabled

**What it does:**
Every time you press `Cmd + S` to save, Prettier automatically formats your code.

**Why it matters:**
You'll never commit messy code again. Professional teams reject pull requests with bad formatting.

**Example:**
You type:

```javascript
const greeting = 'hello';
if (true) {
  console.log(greeting);
}
```

Press `Cmd + S`, it becomes:

```javascript
const greeting = 'hello';
if (true) {
  console.log(greeting);
}
```

#### 2. Tab Size: 2 Spaces

**Setting:** `Editor: Tab Size` → 2

**What it does:**
When you press Tab, it inserts 2 spaces (not 4, not a tab character).

**Why it matters:**
Blockchain code conventions use 2-space indentation. Ethereum's Solidity style guide, Hardhat examples, OpenZeppelin contracts - all use 2 spaces.

#### 3. Auto Save

**Setting:** `Files: Auto Save` → afterDelay

**What it does:**
Automatically saves your file after you stop typing (short delay).

**Why it matters:**
You'll never lose work due to a crash. When testing contracts, you want the latest changes saved automatically.

#### 4. Render Whitespace

**Setting:** `Editor: Render Whitespace` → boundary

**What it does:**
Shows dots for spaces at the end of lines (trailing whitespace).

**Why it matters:**
Trailing whitespace causes Git diffs to show "changed" when nothing actually changed. Linters (code quality tools) flag this as an error.

---

## Part 4: Prettier Configuration (.prettierrc)

### What is .prettierrc?

A configuration file that tells Prettier exactly how to format your code. Different projects have different styles - this file ensures consistency.

### Our Configuration:

```json
{
  "semi": true,
  "trailingComma": "es5",
  "singleQuote": true,
  "printWidth": 80,
  "tabWidth": 2
}
```

### What Each Setting Means:

**`"semi": true`**

- **Means:** Always add semicolons at the end of statements
- **Example:** `const x = 1;` (with semicolon) vs `const x = 1` (without)
- **Why:** JavaScript allows both, but semicolons prevent weird edge cases

**`"trailingComma": "es5"`**

- **Means:** Add commas after the last item in objects/arrays
- **Example:** `{ a: 1, b: 2, }` (with trailing comma)
- **Why:** Makes Git diffs cleaner when you add new properties

**`"singleQuote": true`**

- **Means:** Use single quotes for strings
- **Example:** `'hello'` instead of `"hello"`
- **Why:** Blockchain community convention (Ethereum docs use single quotes)

**`"printWidth": 80`**

- **Means:** Wrap lines longer than 80 characters
- **Why:** GitHub's code viewer is 80 characters wide - code should fit without scrolling

**`"tabWidth": 2`**

- **Means:** Indent with 2 spaces
- **Why:** Matches our Tab Size setting

---

## Part 5: GitHub Integration in VS Code

### What We Did:

Signed into GitHub directly in VS Code so we can commit and push without using terminal commands.

### How Git Integration Works:

**Source Control Panel:**

- Click the branch icon in the sidebar (3rd icon)
- Shows all changed files
- Stage files by clicking **+** icon
- Type commit message at the top
- Click **✓ Commit** button
- Push to GitHub

**Visual Workflow:**

```
1. Edit file → File shows in "Changes"
2. Click + icon → File moves to "Staged Changes"
3. Type message → Describe what you changed
4. Click Commit → Git saves a snapshot
5. Click Push → Uploads to GitHub
```

**Why this matters:**
In production, you'll make dozens of commits per day. Visual Git is faster than typing commands repeatedly.

### Settings Sync:

When we signed into GitHub, we enabled **Settings Sync**. This means:

- Your extensions sync across computers
- Your settings sync across computers
- If you get a new laptop, one click restores your setup

---

## Part 6: First Smart Contract (HelloBlockchain.sol)

### What We Created:

A simple Solidity smart contract to test that our environment works correctly.

### The Contract:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

/**
 * @title HelloBlockchain
 * @dev Simple contract for testing development environment
 */
contract HelloBlockchain {
    string public greeting;

    constructor() {
        greeting = "Hello, Blockchain World!";
    }

    function setGreeting(string memory _greeting) public {
        greeting = _greeting;
    }

    function getGreeting() public view returns (string memory) {
        return greeting;
    }
}
```

### Breaking Down the Code:

**`// SPDX-License-Identifier: MIT`**

- **What it is:** License declaration
- **Why it matters:** Tells others how they can use your code (MIT = open source, anyone can use)
- **Real-world:** Every Ethereum contract needs this or the compiler throws a warning

**`pragma solidity ^0.8.0;`**

- **What it is:** Compiler version requirement
- **Translation:** "This contract requires Solidity version 0.8.0 or higher"
- **Why it matters:** Different Solidity versions have different features. 0.8.0+ has built-in overflow protection

**`contract HelloBlockchain {`**

- **What it is:** Contract declaration (like `class` in other languages)
- **Why it matters:** Everything inside `{}` is part of this contract

**`string public greeting;`**

- **What it is:** A state variable (stored on the blockchain)
- **`string`:** Data type (text)
- **`public`:** Anyone can read this variable
- **Why it matters:** Public variables automatically get a "getter" function

**`constructor() {`**

- **What it is:** Function that runs once when contract is deployed
- **Why it matters:** Initializes the contract's starting state
- **Example:** Sets greeting to "Hello, Blockchain World!" when deployed

**`function setGreeting(string memory _greeting) public {`**

- **What it is:** A function that changes the greeting
- **`string memory _greeting`:** Takes a string as input (stored temporarily in memory)
- **`public`:** Anyone can call this function
- **Why it matters:** This is how users interact with your contract

**`function getGreeting() public view returns (string memory) {`**

- **What it is:** A function that reads the greeting
- **`view`:** Doesn't modify anything (read-only)
- **`returns (string memory)`:** Gives back a string
- **Why it matters:** View functions don't cost gas (they're free to call)

### What We Verified:

- ✅ Syntax highlighting works (keywords are colored)
- ✅ No red error lines (Solidity extension recognizes valid code)
- ✅ File saved in `contracts/` folder
- ✅ Extension shows "Solidity" in the breadcrumb trail

**Why this test matters:**
If syntax highlighting works, it means we can develop smart contracts locally before deploying (saving gas fees on failed deployments).

---

## Part 7: Node.js Verification

### What is Node.js?

JavaScript runtime that lets you run JavaScript outside the browser. Required for:

- Hardhat (smart contract testing framework)
- Ethers.js (library for interacting with Ethereum)
- Web3.js (another Ethereum library)
- Package management (npm)

### Our Versions:

- **Node.js:** v24.6.0 (latest stable release)
- **npm:** 11.5.2 (package manager)

### Why These Matter:

**Node.js:**

- Runs deployment scripts
- Executes automated tests
- Powers local blockchain networks (Hardhat Node)

**npm (Node Package Manager):**

- Installs libraries like `ethers`, `hardhat`, `@openzeppelin/contracts`
- Manages dependencies
- Runs scripts (`npm run deploy`, `npm test`)

**Example workflow we'll use later:**

```bash
npm install hardhat          # Installs Hardhat framework
npx hardhat compile          # Compiles smart contracts
npx hardhat test             # Runs automated tests
npx hardhat node             # Starts local blockchain
```

---

## Part 8: Debug Configuration (launch.json)

### What We Created:

A debugging configuration file that tells VS Code how to debug blockchain scripts.

### The Configuration:

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Debug Blockchain Scripts",
      "skipFiles": ["<node_internals>/**"],
      "program": "${workspaceFolder}/scripts/${fileBasename}"
    }
  ]
}
```

### What This Enables:

**Breakpoints:**

- Click left of line number to add a red dot
- Code pauses when it hits that line
- You can inspect variables at that exact moment

**Step-by-step execution:**

- Run code line by line
- See exactly what each line does
- Catch bugs before they cost gas

**Variable inspection:**

- Hover over variables to see their values
- Check if calculations are correct
- Verify data before sending transactions

**Why this matters:**
Imagine deploying a payment contract with a bug. Every transaction fails, users complain, you lose credibility. Debugging catches this before deployment.

---

## Part 9: Essential Keyboard Shortcuts

### Why Learn Shortcuts?

Professional developers use keyboard shortcuts constantly. Using a mouse is slow - shortcuts make you 2-3x faster.

### Shortcuts We Practiced:

| Shortcut             | What It Does        | When You Use It                                       |
| -------------------- | ------------------- | ----------------------------------------------------- |
| `Cmd + Shift + P`    | **Command Palette** | Access any VS Code feature by typing                  |
| `Cmd + P`            | **Quick Open**      | Jump to any file instantly (type part of filename)    |
| `Cmd + F`            | **Find**            | Search in current file                                |
| `Shift + Option + F` | **Format Document** | Make code look professional instantly                 |
| `` Ctrl + ` ``       | **Toggle Terminal** | Show/hide terminal without using mouse                |
| `Cmd + /`            | **Comment Line**    | Add/remove comments quickly                           |
| `Cmd + D`            | **Multi-cursor**    | Select next occurrence (edit multiple places at once) |
| `Cmd + S`            | **Save**            | Save current file (+ auto-format if enabled)          |

### Real-World Example:

You need to rename a variable in 10 places:

- **Slow way:** Find and click each one (30 seconds)
- **Fast way:** `Cmd + D` repeatedly (3 seconds)

---

## Key Takeaways

### What We Learned:

1. **VS Code is the industry standard** - Every blockchain company uses it
2. **Extensions add blockchain-specific powers** - Solidity highlighting, Hardhat integration
3. **Prettier ensures professional code** - No more messy formatting
4. **Git integration saves time** - Commit without leaving the editor
5. **Syntax highlighting catches errors early** - Before expensive deployments
6. **Node.js powers blockchain tools** - Required for Hardhat, Ethers.js, testing
7. **Debugging prevents costly mistakes** - Catch bugs before deploying to mainnet
8. **Shortcuts make you faster** - Professional developers rarely use a mouse

### Why Today Matters:

Yesterday we set up Git and learned blockchain fundamentals. Today we set up the **workspace** where we'll build payment systems for the next 13 weeks.

Every line of code you write going forward will be in this environment. Time invested in setup pays dividends throughout the program.

---

## Troubleshooting Reference

### Common Issues & Solutions:

**Issue:** Syntax highlighting doesn't work

- **Solution:** Check Extensions panel, ensure Solidity is installed and enabled
- **How to check:** Extensions icon → Search "Solidity" → Should say "Disable" not "Install"

**Issue:** Format on Save doesn't work

- **Solution:** Verify Prettier is installed + .prettierrc exists + setting enabled
- **How to verify:** `Cmd + ,` → Search "format on save" → Should be checked

**Issue:** Can't push to GitHub from VS Code

- **Solution:** Check if signed into GitHub account
- **How to verify:** Accounts icon (bottom-left) → Should show "InnocentKan (GitHub)"

**Issue:** Terminal doesn't open

- **Solution:** Press `` Ctrl + ` `` or `View → Terminal`

**Issue:** Node.js commands not found

- **Solution:** Restart VS Code after installing Node.js
- **How to verify:** Run `node --version` in terminal

---

## Files Created Today

```
Blockchain/
├── .prettierrc                   # Prettier configuration
├── .vscode/
│   └── launch.json               # Debug configuration
├── contracts/
│   └── HelloBlockchain.sol       # Test smart contract
└── week0/
    ├── day1-complete.md          # Yesterday's documentation
    ├── day2-setup.md             # Today's progress notes
    └── day2-complete.md          # This file (full documentation)
```

---

## Next Steps (Day 3 Preview)

Tomorrow we'll learn **Python basics** specifically for blockchain:

- Making API calls to Ethereum nodes
- Parsing JSON responses from blockchain APIs
- Error handling (what if the node is down?)
- Reading transaction data programmatically

**Why Python for blockchain:**

- Most blockchain APIs support Python
- Data analysis (gas prices, transaction volumes)
- Backend services (payment processors, alert systems)
- Smart contract testing scripts

**Estimated time:** 2 hours

---

**Completed:** November 10, 2025  
**Repository:** https://github.com/InnocentKan/blockchain-course  
**Status:** ✅ Professional blockchain development environment ready  
**Next:** Week 0 Day 3 - Python basics for blockchain APIs
