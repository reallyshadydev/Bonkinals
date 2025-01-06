# Bonkinals

A minter and protocol for inscriptions on Bonkcoin.

---

## ⚠️⚠️⚠️ Important ⚠️⚠️⚠️

Use this wallet **ONLY** for inscribing. Avoid storing Bonkinals in Bonkcoin Core.

- Always use a fresh paper wallet for minting until dedicated Bonkinals wallet support is available.
- This wallet is **not** intended for storing funds or inscriptions.

---

## Prerequisites

To use Bonkinals, you will need:
- A fully synced **Bonkcoin node**.
- This repository cloned locally.
- Node.js installed on your system.

---

### 1. Setup Bonkcoin Node

Install Bonkcoin Core from the official GitHub repository:

[Bonkcoin Core Releases](https://github.com/Bonkcoin/Bonkcoin-core/releases)

#### ⚠️⚠️⚠️ Important ⚠️⚠️⚠️

Before syncing your node, create a configuration file:

1. Stop your Bonkcoin node.
2. Create a file named `bonkcoin.conf` in your Bonkcoin data folder.
3. Add the following content to the file, replacing the username (`rpcuser`) and password (`rpcpassword`) with your own secure values:
    ```
    rpcuser=bonker
    rpcpassword=bonkers
    rpcport=14327
    server=1
    listen=1
    txindex=1
    rpcallowip=127.0.0.1
    ```
4. Start your node again.
5. Wait for your node to fully sync with the Bonkcoin network.

---

### 2. Install Node.js

Download Node.js from [Node.js Downloads](https://nodejs.org/en/download) and follow the installation instructions for your operating system.

---

### 3. Setup Bonkinals

#### Clone the Repository

Run the following commands in your terminal:
```bash
cd
git clone https://github.com/Bonkcoin/Bonkinals.git
```

#### Install Dependencies

```bash
cd Bonkinals
npm install
cd bitcore-lib-bonk
npm install
cd ..
```

#### Configure Environment

Create a `.env` file in the `Bonkinals` directory with your node's details:
```env
NODE_RPC_URL=http://127.0.0.1:14327
NODE_RPC_USER=bonker
NODE_RPC_PASS=bonkers
TESTNET=false
```

---

## Managing Wallet Balance

### Generate a New Wallet
```bash
node . wallet new
```

Your private key will be stored in `.wallet.json`. To use it with Bonkcoin Core:

```bash
bonkcoin-cli importprivkey <your_private_key> <optional_label> false
```

Send BONK to the displayed address, then sync your wallet:
```bash
node . wallet sync
```

### Split UTXOs
For frequent minting, split your UTXOs into smaller amounts:
```bash
node . wallet split <count>
```

### Send Funds Back
After minting, you can send remaining funds back:
```bash
node . wallet send <address> <optional amount>
```

---

## Minting Bonkinals

### Inscribe a File

**From a file:**
```bash
node . mint <address> <path>
```

**From raw data:**
```bash
node . mint <address> <content type> <hex data>
```

#### Examples:
```bash
node . mint BbB1ocks3ozcti7m5a3i2wViSuFAchLm3n bonk.jpeg
```

```bash
node . mint BbB1ocks3ozcti7m5a3i2wViSuFAchLm3n "text/plain;charset=utf-8" 426f6e6b426f6e6b426f6e6b
```

---

## Deploying and Minting BNK-20 Tokens

### Deploy BNK-20
```bash
node . bnk-20 deploy <address> <ticker> <max token supply> <max allowed mint limit>
```

#### Example:
```bash
node . bnk-20 deploy BbB1ocks3ozcti7m5a3i2wViSuFAchLm3n BONK 1000 100
```

---

### Mint BNK-20
```bash
node . bnk-20 mint <address> <ticker> <amount>
```

#### Example:
```bash
node . bnk-20 mint BbB1ocks3ozcti7m5a3i2wViSuFAchLm3n BONK 100
```

---

## Viewing Bonkinals

Start the server:
```bash
node . server
```

Open your browser to view an inscription:
```
http://localhost:3000/tx/<transaction_id>
```

#### Note:
Currently, large Bonkinal files may not preview correctly. A fix or indexer update is in progress. Smaller inscriptions are unaffected.

---

## Bonkinals Protocol

The Bonkinals protocol allows inscriptions of any size onto Bonkcoin's blockchain.

### Inscription Example:
```text
"ord"
OP_1
"text/plain;charset=utf-8"
OP_0
"Bonk!"
```

### Multi-Part Content
Content can span multiple parts:
```text
"ord"
OP_2
"text/plain;charset=utf-8"
OP_1
"Bonk and "
OP_0
"bonk bonk bonk!"
```
This would be concatenated into:
```
"Bonk and bonk bonk bonk!"
```

### P2SH Encoding
Inscriptions use P2SH encoding. Redeem scripts must start with inscription push data.

### Chained Transactions
Inscriptions can chain across multiple transactions. Each subsequent part must decrement the number separator until it reaches `OP_0`.

---

## Troubleshooting

### ECONNREFUSED Errors
Ensure your `bonkcoin.conf` file is correct:
```conf
rpcuser=bonker
rpcpassword=bonkers
rpcport=14327
server=1
listen=1
txindex=1
rpcallowip=127.0.0.1
```

Your `.env` file should match:
```env
NODE_RPC_URL=http://127.0.0.1:14327
NODE_RPC_USER=bonker
NODE_RPC_PASS=bonkers
TESTNET=false
```

### Other Issues
Restart your Bonkcoin node or consult the community for assistance.

---

Have fun with Bonkinals!
```

