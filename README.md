# CryptoCurrency Flow Tracking Tool

A simple, easy-to-understand front-end tool to visualize and analyze cryptocurrency transaction flows. This project helps users trace how funds move between addresses and contracts, identify patterns, and get a high-level view of token or coin movements.

Built with:
- JavaScript (front-end logic) — ~75% of the repo
- CSS (styling) — ~21%
- HTML (UI) — ~3%

This README gives step-by-step instructions to run the app locally, explains the main features, shows example usage, and provides development and contribution guidance.

---

What this tool does
- Visualizes the flow of cryptocurrency from a starting wallet or contract.
- Fetches transaction data (via blockchain explorer APIs or nodes), aggregates transfers, and draws a simple graph or list view to help understand fund movement.
- Useful for investigating where large transfers go, following token flows, or learning flow patterns.

Key features
- Enter a wallet address or contract address as the starting point.
- Follow outgoing or incoming transfers for a configurable depth.
- Show token transfers and/or native coin transfers (if supported by data source).
- Simple visual output (graph, table, or timeline) that is easy to read.
- Lightweight front-end (HTML/CSS/JS) — can be run as a static site or with a minimal local server.

Quick demo (what to expect)
- Enter a wallet address in the input box.
- Select direction: Outgoing / Incoming / Both.
- Choose the depth (how many hops to follow).
- Click "Trace" — the app loads transactions and shows a flow chart (or list) with links to transaction details and aggregated amounts.

---

Prerequisites
- A modern browser (Chrome, Edge, Firefox, Safari).
- If running from source:
  - Node.js (>= 12) and npm — only if you plan to run a local dev server or if the project includes build tooling.
  - Or any static file server (live-server, http-server) for serving HTML/CSS/JS.

Optional:
- API keys for blockchain explorers (Etherscan, BscScan, Polygonscan, etc.) for higher rate limits and richer token transfer data.

---

Install & run

Method A — Quick static run (no build step)
1. Clone the repo:
   git clone https://github.com/Sarankishore24/CryptoCurrency-Flow-Tracking-Tool.git
2. Open the project folder and open index.html in your browser:
   - Double-click index.html, or
   - Serve it with a lightweight server (recommended to avoid CORS issues):
     - Using npm http-server:
       npm install -g http-server
       http-server . -p 8080
     - Or using VS Code Live Server extension.
3. Visit http://localhost:8080 (or file:// path) and use the UI.

Method B — Run with Node.js (if package.json exists)
1. Clone the repo:
   git clone https://github.com/Sarankishore24/CryptoCurrency-Flow-Tracking-Tool.git
2. Install dependencies:
   cd CryptoCurrency-Flow-Tracking-Tool
   npm install
3. Start the dev server:
   npm start
4. Open http://localhost:3000 (or the port printed in console).

If the repository doesn't include package.json or start scripts, use Method A.

---

Configuration (API keys & endpoints)

To fetch blockchain data reliably you may need to supply API keys:
- Common providers: Etherscan, BscScan, Polygonscan, Blockchair, Alchemy, Infura.
- Look for a config file or variables (examples: config.js, src/config.js, .env.example).
- Typical patterns:
  - config.js
    const CONFIG = {
      ETHERSCAN_API_KEY: 'your_api_key_here',
      NETWORK: 'ethereum',
      API_BASE_URL: 'https://api.etherscan.io/api'
    }
  - .env (for build/tooling)
    REACT_APP_ETHERSCAN_API_KEY=your_api_key_here

If there is no config file, create a small file (e.g., config.js) and ensure the app imports or reads it.

Rate limits and CORS
- Public APIs often have rate limits. If you hit them, consider using an API key or a proxy that you control.
- When using the app from file:// or a different origin, CORS may block API calls. Serve the files from localhost to avoid problems.

---

Usage guide

1. Start the app in your browser.
2. Enter the address you want to investigate:
   - For Ethereum-style addresses: 0x...
   - For other chains, use their native address formats if supported.
3. Select:
   - Direction: Outgoing / Incoming / Both
   - Depth: How many hops to follow (1 = direct transfers only, 2 = follow the addresses that received/sent from the first hop, etc.)
   - Token filter (optional): show only native coin or a specific token contract address.
4. Click Trace / Analyze:
   - The app will fetch transactions and display results.
   - Results view:
     - Graph: nodes are addresses or contracts; edges show transfer amounts and counts.
     - Table: rows listing transactions with hash, from, to, amount, timestamp.
5. Click a node or tx hash to open the transaction on an explorer in a new tab.

Example:
- Trace 0x123... with Depth = 2 and Direction = Outgoing
  - You see immediate outgoing transfers (hop 1).
  - For addresses that received funds (hop 1), you see their outgoing transfers (hop 2), allowing you to see where the funds ultimately landed.

Interpretation tips
- Look for high-volume nodes (many incoming/outgoing transfers) — they may be exchanges, mixers, or contracts.
- Repeated small transfers to a single address can indicate aggregation.
- Large single transfers might show direct movement to custodial addresses.

---

Project structure (recommended / common)
If your repo follows a common static app layout, you might see:
- index.html — main page
- css/ or styles/ — CSS files
- js/ or src/ — JavaScript logic
- assets/ — images or icons
- config.js or .env.example — configuration and API keys
- README.md — this file

If your repo uses a framework (React/Vue), structure will be different (src/, public/, package.json). Inspect the repository root to adapt these instructions.

---

Development tips

- Use browser devtools (Console / Network) to debug API calls and view errors.
- Add caching for repeated API queries during a session to reduce rate limit issues.
- Paginate transaction fetches (many addresses have thousands of txs).
- Use visualization libraries for graphs:
  - Lightweight: vis.js, cytoscape.js, sigma.js, D3.js
- Be mindful of performance when depth is high; number of nodes can grow exponentially.
- Add UI controls to limit nodes or collapse “small” flows.

Testing
- Manually test with well-known addresses (exchanges, EOA with public txs).
- If the repo has test scripts, run:
  npm test
  (Only if tests exist.)

Accessibility & UX
- Make labels and inputs clear.
- Provide loading states and graceful error messages when APIs fail.

---

Suggested process:
1. Fork the repository.
2. Create a feature branch: git checkout -b feat/your-feature
3. Make changes, run and test locally.
4. Commit and push: git push origin feat/your-feature
5. Open a pull request describing what you changed and why.

Please follow a consistent code style and include comments where behavior is non-obvious.

---

Security & privacy notes

- This tool queries public blockchain data — nothing private is required.
- Do not store private keys or seed phrases anywhere in the project.
- If you add a backend to sign transactions or query private endpoints, secure API keys and secrets using environment variables and never commit them.
- Be careful when opening links to external explorers — ensure they are trusted.

---

Contact / Support

Created by: Sarankishore24 (GROOT)
