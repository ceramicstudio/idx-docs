# Installation

Install the [IDX SDK](../learn/packages.md#idx-sdk) and set up your project.

!!! example ""

    :octicons-alert-16: IDX is in alpha. Libraries may be unstable and APIs are subject to change. Data created on IDX during alpha will *not* be portable to production. Please share what you're working on and report any issues in the [IDX Discord](https://chat.idx.xyz).

<!-- Once [Ceramic Network](https://ceramic.network) launches mainnet in late Q1 2021, IDX will move to production. -->

## **Installation**

Install the [IDX SDK](../learn/packages.md#idx-sdk) and the [Ceramic HTTP client](https://developers.ceramic.network/reference/javascript/clients/#http-client) using npm.

```bash
npm install @ceramicnetwork/http-client @ceramicstudio/idx
```

## **Setup**

### Import dependencies

Import [Ceramic](../learn/glossary.md#ceramic) and IDX by adding these lines to a JavaScript file in your project.

```js
import Ceramic from '@ceramicnetwork/http-client'
import { IDX } from '@ceramicstudio/idx'
```

### Set up aliases

Add an `aliases` object to your JavaScript file. This object stores mappings from human-readable [aliases](../learn/glossary.md#alias) to [definitionIDs](../learn/glossary.md#definitionid), making it easier to reference definitions throughout your project.

```js
const aliases = {
  alias1: 'definitionID 1',
  alias2: 'definitionID 2',
}
```

> Visit [adding aliases](aliases.md) to learn how to add definitions to this list.

### Create instances

Create instances of `ceramic` and `idx` by adding these lines to your JavaScript file. These instances will be used when interacting with the Ceramic and IDX APIs.

```js
const ceramic = new Ceramic('https://yourceramicnode.com')
const idx = new IDX({ ceramic, aliases })
```

### Set your Ceramic node

Set the HTTP URL of the Ceramic node you are using in your project to your `ceramic` instance above. Ceramic node options:

- Community gateway `https://gateway-clay.ceramic.network`: Provides read-only access to the Ceramic Clay testnet. (recommended)

- Community dev node `https://ceramic-clay.3boxlabs.com`: Provides write and read access to the Ceramic Clay testnet. This node is periodically wiped and does not guarantee document persistence. (recommended)

- Run your own node `https://yourEndpoint.com`: Provides write and read access to the Ceramic Clay testnet. Running your own node allows you to persist data and have full control, however this is process is not yet well documented. If you choose to run your own node, be sure to add your node to the Ceramic [`peerlist`](https://github.com/ceramicnetwork/peerlist/blob/main/testnet-clay.json) by submitting a pull request. This allows other nodes to discover your node.

- LocalHost `https://localhost:7007`: Provides read access to the Clay testnet. Writes made to this local node will only be available to nodes in the [`peerlist`](https://github.com/ceramicnetwork/peerlist/blob/main/testnet-clay.json), but will not be available to other nodes on the network. Users need to first have a Ceramic daemon running locally using the CLI.

## **Example**

Your code should look like this:

```js
import Ceramic from '@ceramicnetwork/http-client'
import { IDX } from '@ceramicstudio/idx'

const aliases = {
  alias1: 'definitionID 1',
  alias2: 'definitionID 2',
}

const ceramic = new Ceramic('https://yourceramicnode.com')
const idx = new IDX({ ceramic, aliases })
```
