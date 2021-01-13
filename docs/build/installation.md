# Installation

Install the [IDX SDK](../learn/packages/#idx-sdk) and set up your project.

!!! warning ""

    :octicons-alert-16: IDX is in alpha. Libraries may be unstable and APIs are subject to change. Please share what you're working on and report any issues in the [IDX Discord](https://chat.idx.xyz).

## **Installation**

Install the [IDX SDK](../learn/packages/#idx-sdk) and the [Ceramic HTTP client](https://developers.ceramic.network/reference/javascript/clients/#http-client) using npm.

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

Add an `aliases` object to your JavaScript file. This object stores mappings from human-readable names to [definitions](../learn/glossary.md#definition), making it easier to reference definitions throughout your project using their [aliases](../learn/glossary.md#alias).

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

- Community gateway `https://ceramic-clay-gateway.3boxlabs.com`: Provides read-only access to the Clay testnet.

- Run your own node `https://yourEndpoint.com`: Provides write and read access to the Clay testnet. Running your own node allows you to persist documents and have full control.

- LocalHost `https://localhost:7007`: Provides write and read access to the Clay testnet. Users need to first have a Cermic daemon running locally using the CLI.

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
