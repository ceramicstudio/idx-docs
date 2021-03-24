# Reading records

Use the [`idx.get()`](../reference/idx.md#get) method to query a [record](../learn/glossary.md#record) at runtime.

## **Using default aliases**

Pass an alias from [default definitions](../guides/definitions/default.md), and the [DID](../learn/glossary.md#did) or [Blockchain Account ID](../learn/glossary.md#caip-10-account-id) that you wish to query.

For example if you want to query IDX data from the ethereum account `0xab16a96d359ec26a11e2c2b3d8f8b8942d5bfcdb` on mainnet you can simply use the string `0xab16a96d359ec26a11e2c2b3d8f8b8942d5bfcdb@eip155:1`.

```js
await idx.get('basicProfile', '<DID-or-caip10-id>')
```

[:octicons-file-code-16: API reference](../reference/idx.md#get)

## **Using your aliases**

Pass as alias from your `aliases` object, and the [DID](../learn/glossary.md#did) or [Blockchain Account ID](../learn/glossary.md##caip-10-account-id) that you wish to query.

```js
await idx.get('myAlias', '<DID-or-caip10-id>')
```

[:octicons-file-code-16: API reference](../reference/idx.md#get)

## **Authenticated users**

If a user is currently [authenticated](authentication.md) to your application, you only need to pass an alias. When no DID is provided, IDX will default to the DID of the currently authenticated user.

```js
await idx.get('myAlias')
```

[:octicons-file-code-16: API reference](../reference/idx.md#get)

## **Example**

=== "Method call"

    ```js
    await idx.get('basicProfile')
    ```

=== "Returned value"

    ```js
    {
      name: 'Alan Turing',
      description: 'I make computers beep good.',
      image: '',
      emoji: '💻'
    }
    ```
