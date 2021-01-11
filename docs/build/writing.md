# Writing records

Use the [`idx.set()`]() method to create or modify a [record]() at runtime. Writing to records requires having an [authenticated user]().

## **Using default aliases**

Pass an alias from [default aliases]() and the data that you wish to write to the record.

```js
await idx.set(`basicProfile` { content })
```

[:octicons-file-code-16: API reference]()

## **Using your aliases**

Pass an alias from your `aliases` object and the data that you wish to write to the record.

```js
await idx.set(`myAlias` { content })
```

[:octicons-file-code-16: API reference]()

## **Example**

=== "Request"

```js
await idx.set(`basicProfile`, {
  name: 'Alan Turing',
  description: 'I make computers beep good.',
  emoji: '💻',
})
```

=== "Response"

`DocID` of the record
