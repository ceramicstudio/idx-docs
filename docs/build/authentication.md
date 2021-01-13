# Authentication

Authentication allows you to [write records](writing.md) or [read encrypted records](reading.md). If you only need to read plaintext records, then you **do not** need authentication.

## **How it works**

IDX uses [DIDs](../reference/dependency-apis.md#did) for identifiers and authentication. Once a DID is authenticated using a [DID provider](../reference/dependency-apis.md#didprovider), the authenticated DID provider needs to be set to the [Ceramic instance]() used by your project. This will allow the user to perform authenticated transactions on IDX using their DID such as [writing records](writing.md) and [reading enctypted records](reading.md).

## **Prerequisites**

In order to add authentication, you must have [installed the IDX SDK](../reference/idx.md).

## **Installation**

Jump over to the [**Ceramic documentation** :octicons-link-external-16:]() to learn how to add authentication to your project.

## **Example**

After you have set the authenticated DID provider on the `ceramic` instance you can interact with your `idx` instance in an authenticated way. If configured correctly, it will look something like this:

```js
await ceramic.setDIDProvider(...)
await idx.get('anAlias') // uses authenticated DID
```
