# ⚖️ GenMarket AI: Autonomous Prediction Markets on GenLayer

GenMarket AI is a decentralized prediction market protocol powered by GenLayer's Intelligent Contract framework. By leveraging GenLayer's unique non-deterministic compute platform, the contract reads real-world web data directly from the internet and utilizes decentralized multi-node LLM consensus to resolve complex text-based prediction markets—eliminating the need for centralized intermediaries or static oracle networks.

---

## 🏛️ System & Consensus Architecture

Traditional prediction markets (like Polymarket) rely on manual, centralized resolutions or game-theoretic multi-chain disputes when market endpoints are ambiguous. GenMarket AI utilizes **GenLayer's Optimistic Democracy** consensus protocol to process subjective language data and non-deterministic web responses securely on-chain.


```

```
   [ 🧑‍💻 User Prompt ] -> (Create Unambiguous Market Structure)
                                  |
                                  v

```

+-------------------------------------------------------------------------+
|                  🤖 GENVM VALIDATOR CONSENSUS ROUND                     |
|                                                                         |
|  1. gl.nondet.web.render()  --> Scrapes real-time web news raw data     |
|  2. gl.nondet.exec_prompt() --> Runs strict, independent AI evaluations |
|  3. gl.eq_principle.strict_eq() --> Reaches strict cryptographic balance|
+-------------------------------------------------------------------------+
|
v
[ 📝 Settle State ] -> Trigger Automatic Token Payout Dispatches

```

### Key Technical Primitives Used:
* **Single-TreeMap Monolith Pattern (`TreeMap[str, str]`)**: Optimized state layout tracking all configuration metadata, parimutuel pools, and stakeholder index vectors using uniquely prefixed key paths inside a solitary blockchain tree instance.
* **Non-Deterministic Web Scraping (`gl.nondet.web.render`)**: Validators independently render live web assets directly at runtime, trimming down context structures to feed consensus execution.
* **Equivalence Principle Validation (`gl.eq_principle.strict_eq`)**: Enforces consensus guarantees across heterogeneous node clusters executing AI logic, throwing out transaction frames if inferences diverge.
* **Native Value Escrows (`gl.actions.transfer`)**: Handles real liquidity by transforming parimutuel trading pools directly into secure native token distributions to verified predicting accounts.

---

## 📁 Repository Blueprint

```text
├── .github/workflows/
│   └── genvm-ci.yml       # Automated validation pipelines for GenVM contracts
├── contracts/
│   └── gen_market_ai.py   # Refactored Single-TreeMap Contract (Python)
├── src/
│   ├── components/
│   │   ├── TradingPanel.tsx   # React Order panel executing `buy_shares`
│   │   └── ResolutionView.tsx # Adjudication logs & payout claims UI
│   └── lib/
│       └── genlayerClient.ts  # genlayer-js client connection setup
├── package.json           # Frontend framework and CLI runtime tools
└── README.md              # Project documentation

```

---

## 🚀 Local Network Sandbox Setup

Follow these setup steps to execute, test, and deploy the application locally.

### Prerequisites

* **Node.js**: `v18.x` or higher
* **Python**: `v3.12.x`
* **Docker Engine**: `v26.x` or higher (Required for the local node cluster runner)

### 1. Initialize and Start GenLayer Localnet

Install the GenLayer Global CLI tool and spin up the Docker-based local node infrastructure:

```bash
# Install the GenLayer CLI globally
npm install -g genlayer

# Download and initialize the local cluster node configurations
genlayer init

# Run the validator consensus layer and spin up sandboxes
genlayer up

```

### 2. Verify and Deploy the Intelligent Contract

Compile and test the contract logic using the GenVM verification tool suite:

```bash
# Install dependencies inside your root repo directory
npm install

# Check for safety compliance, deterministic logic bounds, and TreeMap properties
npm run contract:lint

# Deploy your contract template targeting the local network context
genlayer deploy --contract ./contracts/gen_market_ai.py

```

*Note: Make sure to update the environment file or `src/lib/genlayerClient.ts` with your newly generated deployment address string.*

### 3. Launch the Frontend DApp Engine

Run the development environment to begin testing features through your browser:

```bash
npm run dev

```

Open [http://localhost:3000](https://www.google.com/search?q=http://localhost:3000) to view your DApp workspace.

---

## 📖 Core Contract API & Storage Mechanics

The underlying Python contract relies on a single persistent storage map (`state: TreeMap[str, str]`). Key structures are organized using explicit prefix rules:

| State Path Key | Value Representation | Description |
| --- | --- | --- |
| `"owner"` | `str` (Address) | Address holding administrative control flags |
| `"count"` | `str` (Integer) | Total auto-incrementing market indexing marker |
| `"market:{id}"` | `str` (JSON String) | Comprehensive configuration settings block |
| `"pool:{id}"` | `str` (JSON String) | Parimutuel balance registry mapping `{"yes": int, "no": int}` |
| `"pos:{id}:{addr}"` | `str` (JSON String) | Stake weights recorded per address |

### Write Operations

#### `create_market(prompt: str, expiration_date: str) -> str`

Takes an unstructured market query (e.g., `"Will Ethereum cross $5,000 by Christmas?"`). Validators invoke an LLM to parse this request into title structures, clear categorical conditions, and targeted resolution domains. The operation aborts if the compiled proposal scores below a 50% target clarity rating.

#### `buy_shares(market_id: str, outcome: str) -> str` **[Payable]**

Accepts active native tokens (`gl.message.value`) to buy into the `"YES"` or `"NO"` pool index for a given active prediction market.

#### `trigger_ai_resolution(market_id: str) -> str`

Transitions a market into `DELIBERATING` and fetches live internet source data via `gl.nondet.web.render`. Validating nodes process the raw data text against the market's initial criteria rules using `gl.eq_principle.strict_eq` to securely lock in a consensus outcome (`"YES"`, `"NO"`, or `"UNRESOLVABLE"`).

#### `claim_winnings(market_id: str) -> str`

Enables winning pool predictors to claim their proportional split of the total token value pool. The contract wipes their internal position balance map to protect against re-entrancy, and then uses `gl.actions.transfer` to instantly dispatch the funds back to the user's wallet address.

---

## 🛡️ CI/CD Quality Control

This repository includes a GitHub Actions validation pipeline (`.github/workflows/genvm-ci.yml`). Every codebase push or pull request automatically evaluates your Python code using the `genvm-lint` ruleset. This pipeline catches non-deterministic syntax usage (such as native Python standard time calls or unmapped network loops) before your smart contract hits the blockchain.

```bash
# Run lint tests manually inside your local workflow terminal
genvm-lint check contracts/gen_market_ai.py

```

---
