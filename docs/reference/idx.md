# IDX SDK Reference

## Installation

```sh
npm install @ceramicstudio/idx
```

## IDX class

### **constructor**

**Arguments:**

1. [`options: IDXOptions`](types.md#idxoptions)

### **.authenticated**

Returns whether a [DID](dependency-apis.md#did) is currently [authenticated](../build/authentication.md).

**Returns:** `boolean`

### **.ceramic**

**Returns:** [`CeramicApi`](dependency-apis.md#ceramicapi)

### **.id**

Returns the [DID](dependency-apis.md#did) of the currently authenticated user.

> Accessing this property will throw an error if the instance is not authenticated.

**Returns:** `string`

### **.has()**

Returns whether a [record](../learn/glossary.md#record) exists in the [index](../learn/glossary.md#index) for a given [DID](../learn/glossary.md#did).

**Arguments:**

1. `name: string` ([alias](../learn/glossary.md#alias) or [IndexKey](types.md#indexkey))
1. `did?: string = this.id`

**Returns:** `Promise<boolean>`

### **.get()**

Returns a [record](../learn/glossary.md#record) in the [index](../learn/glossary.md#index) for a given [DID](../learn/glossary.md#did) or [Blockchain Account ID](../learn/glossary.md#caip-10-account-id) .

**Arguments:**

1. `name: string` ([alias](../learn/glossary.md#alias) or [IndexKey](types.md#indexkey))
1. `did?: string = this.id`

**Returns:** `Promise<unknown>`

### **.set()**

Sets or modifies a [record](../learn/glossary.md#record) in the [index](../learn/glossary.md#index) of the authenticated [DID](dependency-apis.md#did).

**Arguments:**

1. `name: string` ([alias](../learn/glossary.md#alias) or [IndexKey](types.md#indexkey))
1. `content: unknown`
1. [`options?: CreateOptions`](types.md#createoptions) (only applied if the record is being created, if it already exists they are ignored)

**Returns:** [`Promise<StreamID>`](dependency-apis.md#streamid) the [recordID](../learn/glossary.md#recordid) of the created [record](../learn/glossary.md#record)

### **.merge()**

Performs a shallow (one level) merge to a [record](../learn/glossary.md#record) in the [index](../learn/glossary.md#index) of the authenticated [DID](dependency-apis.md#did).

**Arguments:**

1. `name: string` ([alias](../learn/glossary.md#alias) or [IndexKey](types.md#indexkey))
1. `content: unknown`
1. [`options?: CreateOptions`](types.md#createoptions) (only applied if the record is being created, if it already exists they are ignored)

**Returns:** [`Promise<StreamID>`](dependency-apis.md#streamid) the [recordID](../learn/glossary.md#recordid) of the created [record](../learn/glossary.md#record)

### **.setAll()**

Similar to the [`.set()`](#set) method but for setting multiple [records](../learn/glossary.md#record) at once in a more efficient way.

> The index will only get updated if all records are successfully set.

**Arguments:**

1. `contents: Record<string, unknown>`
1. [`options?: CreateOptions`](types.md#createoptions) (only applied if the record is being created, if it already exists they are ignored)

**Returns:** `Promise<Record<string, string>>` the [recordIDs](../learn/glossary.md#recordid) of the created [records](../learn/glossary.md#record)

### **.setDefaults()**

Similar to the [`.setAll()`](#setall) method but only sets [records](../learn/glossary.md#record) for keys that are not already present in the [index](../learn/glossary.md#index).

1. `contents: Record<string, unknown>`
1. [`options?: CreateOptions`](types.md#createoptions) (only applied if the record is being created, if it already exists they are ignored)

**Returns:** `Promise<Record<string, string>>` the [recordIDs](../learn/glossary.md#recordid) of the created [records](../learn/glossary.md#record)

### **.remove()**

Removes a [definitionID](../learn/glossary.md#definitionid):[recordID](../learn/glossary.md#recordid) pair from the [index](../learn/glossary.md#index) of the authenticated [DID](dependency-apis.md#did).

**Arguments:**

1. `name: string` ([alias](../learn/glossary.md#alias) or [IndexKey](types.md#indexkey))

**Returns:** `Promise<void>`

### **.getIndex()**

Returns the [index](../learn/glossary.md#index) for the given [DID](../learn/glossary.md#did).

> This method can be used to get the full definitionID:recordID mapping at once

**Arguments:**

1. `did?: string = this.id`

**Returns:** [`Promise<Index | null>`](types.md#index)

### **.iterator()**

Returns an async iterator of [`Entry`](types.md#entry) for the given [DID](../learn/glossary.md#did).

> This method can be used to iteratively load all the records in the index

**Arguments:**
å

1. `did?: string = this.id`

**Returns:** [`AsyncIterableIterator<Entry>`](types.md#entry)

### **.getDefinition()**

Loads a [definition](../learn/glossary.md#index).

**Arguments**:

1. `id: StreamID | IndexKey` ([StreamID](dependency-apis.md#streamid) or [IndexKey](types.md#indexkey))

**Returns:** [`Promise<DefinitionWithID>`](types.md#definitionwithid)

## **getLegacy3BoxProfileAsBasicProfile()**

!!! deprecated ""

    :octicons-alert-16: This function is exposed to help projects transition from 3Box to IDX as a temporary solution. It will be removed from IDX in the future.

Returns a `BasicProfile` object converted from a 3Box profile if existing for the given Ethereum `address`, or `null` if unavailable.

**Arguments:**

1. `address: string`: Ethereum address starting with `0x`

**Returns:** `Promise<BasicProfile | null>`
