---
description: Getting started shouldn't be difficult.
---

# Installation

To get started, install the DSA Connect package from npm:

```bash
npm install nubian-dsa-connect
```

For browsers, via jsDelivr CDN:

```markup
<script src="https://cdn.jsdelivr.net/npm/nubian-dsa-connect@latest/dist/index.bundle.js"></script>
```

## Usage

To enable web3 calls via SDK, instantiate [web3 library](https://github.com/ChainSafe/web3.js#installation)

```javascript
// in browser
if (window.ethereum) {
  window.web3 = new Web3(window.ethereum)
} else if (window.web3) {
  window.web3 = new Web3(window.web3.currentProvider)
} else {
  window.web3 = new Web3(customProvider)
}
```

```javascript
// in nodejs
const Web3 = require('web3')
const DSA = require('nubian-dsa-connect')
const web3 = new Web3(new Web3.providers.HttpProvider(ETH_NODE_URL))
```

Now instantiate DSA with web3 instance.

```javascript
// in browser
const dsa = new DSA(web3)

// in nodejs
const dsa = new DSA({
  web3: web3,
  mode: 'node',
  privateKey: PRIVATE_KEY,
})
```

