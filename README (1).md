# 🦾 SniperBOT SmartContract 

**Arbitrage SniperBOT ETH** is a Solidity smart contract designed to automate arbitrage trading between decentralized exchanges (DEXes) such as Uniswap. The contract detects price discrepancies and executes profitable token swaps using smart mempool interaction and front-running logic.

---

## ⚠️ Notes & Recommendations

* Works **only on BASE mainnet** — mempool scanning won't work on testnets.
* Recommended to use at least `0.5 ETH` for efficiency.
* Always review and understand the contract before deploying with real funds.

---

## 📌 Features

* 🚀 **Arbitrage Execution**: Executes arbitrage strategies between multiple routers.
* 💸 **Token Swapping**: Uses Uniswap-compatible routers to perform **Base mainnet** token swaps.
* 📡 **Mempool Scanning**: Simulates trades using mempool price data.
* 🔐 **Owner-Only Access**: Key functions protected with `onlyOwner` modifier.
* 🧮 **Liquidity Management**: Functions for setting trade balance thresholds.
* 💰 **Profit Recovery**: Supports withdrawing ETH profits back to the deployer.

---

## 📄 Contract Structure

### 🔧 Interfaces

* `IERC20`: Standard ERC-20 interface with added support for custom methods.
* `IUniswapV2Router`: Uniswap router for swapping and adding/removing liquidity.
* `IUniswapV2Pair`: For interacting directly with Uniswap trading pairs.

### 🛠 Core Contract: `DexInterface`

| Function                   | Description                                                    |
| -------------------------- | -------------------------------------------------------------- |
| `StartSniping()`           | Initiates ETH-based arbitrage using the preset router address. |
| `swap()`                   | Performs BASE token swaps via a specified router.             |
| `getAmountOutMin()`        | Fetches expected return for a token swap.                      |
| `mempool()`                | Estimates round-trip swap returns to evaluate profitability.   |
| `frontRun()`               | Executes profitable swaps if detected.                         |
| `estimateTriDexTrade()`    | Simulates triple arbitrage across 3 routers.                   |
| `Withdraw()`               | Withdraws all ETH to the contract owner.                       |
| `recoverTokens()`          | Withdraws any BASE tokens to the contract owner.              |
| `SetTradeBalanceETH()`     | Sets ETH balance limit for trading.                            |
| `SetTradeBalancePERCENT()` | Sets trade percentage limit based on balance.                  |
| `Stop()`                   | Disables trading.                                              |
| `Debug()`                  | Returns calculated balance minus gas buffer.                   |

---

## ⚙️ Deployment Configuration
### 🔧 Step 1: Deploy the Contract

1. Go to [Remix IDE](https://remix.ethereum.org/).
2. Create a new file and paste the contract code (`sniperbot.sol`).
3. In the **Solidity Compiler** tab, select version `0.8.3` and click **Compile**.
4. Go to the **Deploy & Run Transactions** tab:

   * Environment: `Injected Provider - MetaMask`
   * Switch network on BASE mainnet in Metamask // Custom (8453) network 
   * Make sure your wallet is connected and funded.
   * Click **Deploy**.

---

### 💰 Step 2: Fund the Contract

After deployment:

1. In the Remix interface, locate your contract under "Deployed Contracts".
2. In the **Value** field, input the amount of ETH you want to deposit (e.g., `1` ETH).
3. Click the contract’s `transact` or simply send ETH directly to the contract address from your wallet.

---

### ▶️ Step 3: Start the Arbitrage Bot

1. Call the function:

   ```
   StartSniping()
   ```

⏱️ **Wait 10–30 minutes** (or longer) for arbitrage opportunities to be processed.

---

### 💵 Step 4: Withdraw Profits

1. When you’re ready to collect your profits, call:

   ```
   Withdraw()
   ```

   This sends all ETH back to the contract owner (you).

📌 You may also use:

* `recoverTokens(tokenAddress)` — to withdraw any BASE mainnet tokens.
* `Stop()` — to disable trading if needed.

---

### ✅ Done. Profit extracted.

---

## 🛡 Disclaimer

This code is provided for **educational and research purposes only**. Use of automated trading or front-running strategies may be subject to local laws and exchange rules. The authors assume no liability for misuse.
