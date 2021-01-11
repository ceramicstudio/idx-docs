# IDX SDK Reference

## Installation

```sh
npm install @ceramicstudio/idx
```

See the full [installation guide]() to properly install the IDX SDK.

## API

### **constructor**

Arguments:

- `options`: IDXOptions

Returns: `Promise<void>`

=== "Request"

    ```javascript
    ```

=== "Response"

    ```javascript
    ```

---

### **.authenticated**

> Returns whether a [DID]() is currently [authenticated]().

Returns: `boolean`

=== "Request"

    ```javascript
    await idx.authenticated()
    ```

=== "Response"

    ```javascript
    ```

---

### **.ceramic**

Returns: `CeramicApi`

=== "Request"

    ```javascript
    await idx.ceramic()
    ```

=== "Response"

    ```javascript
    ```

---

### **.id**

> Returns the [DID]() of the currently authenticated user.

Accessing this property will throw an error if the instance is not authenticated.

Returns: `string`

=== "Request"

    ```javascript
    await idx.id()
    ```

=== "Response"

    ```javascript
    ```

---

### **.has()**

> Returns whether a [record]() exists in the [index]() for a given [DID]().

Arguments:

- `name`: string ([alias](), [IndexKey]() or [definitionID]())
- `did?`: string = this.id

Returns: `Promise<boolean>`

=== "Request"

    ```javascript
    await idx.has()
    ```

=== "Response"

    ```javascript
    ```

---

### **.get()**

> Returns a [record]() in the [index]() for a given [DID]().

Arguments:

- `name`: string ([alias](), [IndexKey]() or [definitionID]())
- `did?`: string = this.id

Returns: `Promise<unknown>`

=== "Request"

    ```javascript
    await idx.get()
    ```

=== "Response"

    ```javascript
    ```

---

### **.set()**

> Sets or modifies a [record]() in the [index]() of the authenticated [DID]().

Arguments:

- `name`: string ([alias](), [IndexKey]() or [definitionID]())
- `content`: unknown
- `options`?: CreateOptions (only applied if the document is being created, if it already exists they are ignored)

Returns: `Promise<DocID>` the [recordID]() of the created [record]()

=== "Request"

    ```javascript
    await idx.set()
    ```

=== "Response"

    ```javascript
    ```

---

### **.merge()**

> Performs a shallow (one level) merge to a [record]() in the [index]() of the authenticated [DID]().

The provided options are only applied if the document is being created. If it already exists, they are ignored.

Arguments:

- `name`: string ([alias](), [IndexKey]() or [definitionID]())
- `content`: unknown
- `options?`: CreateOptions

Returns: `Promise<DocID>` the [recordID]() of the created [record]()

=== "Request"

    ```javascript
    await idx.merge()
    ```

=== "Response"

    ```javascript
    ```

---

### **.setAll()**

> Similar to the [`.set`](#set) method but for setting multiple [records]() at once in a more efficient way.

The index will only get updated if all records are successfully set.

Arguments:

- `contents`: Record<string, unknown>
- `options?`: CreateOptions

=== "Request"

    ```javascript
    await idx.setAll()
    ```

=== "Response"

    ```javascript
    ```

---

### **.setDefaults()**

> Similar to the [`.setAll`](#setall) method but only sets [records]() for keys that are not already present in the [index]().

Arguments:

- `contents`: Record<string, unknown>
- `options?`: CreateOptions

=== "Request"

    ```javascript
    await idx.setDefaults()
    ```

=== "Response"

    ```javascript
    ```

---

### **.remove()**

> Remove a [definition]():[record]() pair from the [index]() of the authenticated [DID]().

Arguments:

- `name`: string ([alias](), [IndexKey]() or [definitionID]())

Returns: `Promise<void>`

=== "Request"

    ```javascript
    await idx.remove()
    ```

=== "Response"

    ```javascript
    ```

---

### **.getIndex()** (fka .getIDXContent)

> Returns the [index]() for the given [DID]().

Arguments:

- `did?`: string = this.id

Returns: `Promise<IdentityIndexContent | null>`

=== "Request"

    ```javascript
    await idx.getIDXContent()
    ```

=== "Response"

    ```javascript
    ```

---

### **.iterator()**

> Returns an async iterator of ContentEntry for the given DID

Arguments:

- `did?`: string = this.id

Returns: `AsyncIterableIterator<ContentEntry>`

=== "Request"

    ```javascript
    await idx.contentIterator()
    ```

=== "Response"

    ```javascript
    ```

---

### **.getDefinition()**

> Loads a [definition]().

Arguments:

- `id`: string (DocID or IndexKey)

Returns: `Promise<Definition>`

=== "Request"

    ```javascript
    await idx.getDefinition()
    ```

=== "Response"

    ```javascript
    ```
