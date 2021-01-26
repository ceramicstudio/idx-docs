# Writing records

Use the [`idx.set()`](../reference/idx.md#set) method to create or modify a [record](../learn/glossary.md#record) at runtime. Writing to records requires having an [authenticated user](authentication.md). All writes will be performed by that user and applied to their records.

!!! example ""

    :octicons-alert-16: If an existing record is already set, calling `idx.set()` again will completely replace the record contents. Alternatively, it is possible to [merge the existing record contents](#merging-content).

## **Using default aliases**

Pass an alias from [default aliases](../guides/definitions/default.md) and the data that you wish to write to the record.

```js
await idx.set('basicProfile', content)
```

[:octicons-file-code-16: API reference](../reference/idx.md#set)

## **Using your aliases**

Pass an alias from your `aliases` object and the data that you wish to write to the record.

```js
await idx.set('myAlias', content)
```

[:octicons-file-code-16: API reference](../reference/idx.md#set)

## **Example**

=== "Method call"

    ```js
    await idx.set('basicProfile', {
      name: 'Alan Turing',
      description: 'I make computers beep good.',
      emoji: '💻',
    })
    ```

=== "Returned value"

    ```
    recordID of the record
    ```

## **Merging content**

Calling `idx.set()` on an existing record completely replaces the existing content. If you want to keep the existing content and only change some fields, [`idx.merge()`](../reference/idx.md#merge) can be used instead.

=== "First method call"

    ```js
    await idx.set('basicProfile', { name: 'Alan Turing' })
    ```

=== "Second method call"

    ```js
    await idx.merge('basicProfile', { emoji: '💻' })
    ```

=== "Resulting record"

    ```js
    {
      name: 'Alan Turing',
      emoji: '💻',
    }
    ```

[:octicons-file-code-16: API reference](../reference/idx.md#merge)
