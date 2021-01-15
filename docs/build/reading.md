# Reading records

Use the [`idx.get()`](../reference/idx.md#get) method to query a [record](../learn/glossary.md#record) at runtime.

## **Using default aliases**

Pass an alias from [default definitions](../guides/definitions/default.md) and the DID that you wish to query.

```js
await idx.get('basicProfile', '<DID>')
```

[:octicons-file-code-16: API reference](../reference/idx.md#get)

## **Using your aliases**

Pass as alias from your `aliases` object and the DID that you wish to query.

```js
await idx.get('myAlias', '<DID>')
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
