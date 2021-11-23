---
description: Getting started shouldn't be difficult.
---

# Installation and Setup

### Installation

To get started, install the Nubian coven SDK package from npm:

```bash
npm install nubian-coven-sdk
```

### Usage

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
const NUB = require('nubian-coven-sdk')
const web3 = new Web3(new Web3.providers.HttpProvider(BSC_NODE_URL))
```

Now instantiate NUB with web3 instance.

```javascript
// in browser
const nub = new NUB(web3)

// in nodejs
const nub = new NUB({
  web3: web3,
  mode: 'node',
  privateKey: PRIVATE_KEY,
})
```
