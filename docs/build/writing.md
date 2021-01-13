# Writing records

Use the [`idx.set()`](../reference/idx.md#set) method to create or modify a [record](../learn/glossary.md#record) at runtime. Writing to records requires having an [authenticated user](authentication.md).

## **Using default aliases**

Pass an alias from [default aliases](../guides/definitions/default.md) and the data that you wish to write to the record.

```js
await idx.set(`basicProfile`, { content })
```

[:octicons-file-code-16: API reference](../reference/idx.md#set)

## **Using your aliases**

Pass an alias from your `aliases` object and the data that you wish to write to the record.

```js
await idx.set(`myAlias`, { content })
```

[:octicons-file-code-16: API reference](../reference/idx.md#set)

## **Example**

=== "Method call"

    ```js
    await idx.set(`basicProfile`, {
      name: 'Alan Turing',
      description: 'I make computers beep good.',
      emoji: '💻',
    })
    ```

=== "Returned value"

    `DocID` of the record
