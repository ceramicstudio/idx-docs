# Reading records

Use the [`idx.get()`]() method to query a [record]() at runtime.

## **Using default aliases**

Pass an alias from [default definitions]() and the DID that you wish to query.

```js
await idx.get(`basicProfile`, '<DID>')
```

[:octicons-file-code-16: API reference]()

## **Using your aliases**

Pass as alias from your `aliases` object and the DID that you wish to query.

```js
await idx.get(`myAlias`, '<DID>')
```

[:octicons-file-code-16: API reference]()

## **Authenticated users**

If a user is currently [authenticated]() to your application, you only need to pass an alias. When no DID is provided, IDX will default to the DID of the currently authenticated user.

```js
await idx.get(`myAlias`)
```

[:octicons-file-code-16: API reference]()

## **Example**

=== "Request"

```js
await idx.get(`basicProfile`)
```

=== "Response"

```js
{
  name: 'Alan Turing',
  description: 'I make computers beep good.',
  image: '',
  emoji: '💻'
}
```
