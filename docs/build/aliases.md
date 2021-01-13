# Adding aliases

Add the [definitionIDs](../learn/glossary.md#definitionid) used by your application to the `aliases` object in your JavaScript file. This will allow you to [read records](reading.md) and [write records](writing.md) using human-readable [aliases](../learn/glossary.md#alias).

## **Default aliases**

IDX comes prepackaged with a set of default definitions and corresponding aliases that you can use within your project to read or write to records without any additional configuration or set up. These **do not** need to be added to your `alias` object and their aliases can be used automatically.

To understand what's included, view [**default definitions**](../guides/definitions/default.md).

!!! example ""

    **Use case: Read or write to a universal user profile**

IDX includes a `basicProfile` alias that allows you to read or write to a basic user profile without needing to worry about definitions or aliases.

## **Custom aliases**

If you want to do more with IDX than what's inclued in default definitions, you will need to gather existing definitions or create new definitions and then add them to your `aliases` object.

```js
const aliases = {
  alias1: 'definitionID 1',
  alias2: 'definitionID 2',
}
```

### Using existing definitions

If you want to read or write to records that already exist and have been created by third-party applications, then you will need to reuse existing definitions and add them to your `aliases` object. Reusing definitions encourages cross-platform data interoperability by converging on definitions and schema standards specific to certain use cases. After discovering definitions, you will need to add them to your `aliases` object.

There are various ways to discover definitions, see [**discovering definitions**](../guides/definitions/discovering.md).

!!! example ""

    **Use case: Display blog posts created in another application**

For a simple demonstration, let's consider a use case where two different applications want to display the blog posts created by a user. Both applications would need to read the same definition that contains the list of the user's blog posts.

### Using new definitions

If you are not able to use default or existing definitions in your project, then you will need to create new definitions. Creating new definitions allows you to create and interact with records specifically suited to the needs of your application. After creating definitions, you will need to add them to your `aliases` object.

For a step by step guide, see [**creating definitions**](../guides/definitions/creating.md).
