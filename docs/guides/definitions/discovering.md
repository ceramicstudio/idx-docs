# Existing definitions

When deciding which [definitions](../../learn/glossary.md#definition) to use in your project, you might consider utilizing existing definitions. Existing definitions allow your application to [read records](../../build/reading.md) and [write records](../../build/writing.md) originally created by another application. This enables simple cross-application data sharing.

## **Ways to discover definitions**

There are two primary mechanisms for discovering existing definitions:

- [Inspect the indexes]() of known DIDs to see which definitions they have
- [Inspect the Github repos]() of open source projects to see which definitions they're using

## **Inspecting indexes**

Use the [IDX CLI](../../reference/cli.md) to inspect the [indexes](../../learn/glossary.md#index) of known DIDs.

### Prerequisites

- You must have a properly configured IDX CLI. See [using the CLI](../../guides/cli.md) to get started.
- You must have a list of known DIDs that are relevant to your application, such as existing users or target users. You can get creative assembling this list using any means available to you. It's worth noting that many 3ID DIDs have blockchain accounts publicly linked to their DID, which can be used to lookup their DID from their blockchain account.

### List all definitions

Use the `idx index:inspect` command to view all definitions included in the index for a given DID:

```bash
idx index:inspect <UserDID>
```

=== "Example command"

    ```bash
    idx index:inspect did:3:kjzl6cwe1jw14as9oy1pu5w1ufl7gxry095b7srr0m4y04n22e8vjliklpdvewv
    ```

=== "Example response"

    ```bash
    ✔ IDX document loaded
    ✔ kjzl6cwe1jw14blngzz896wlixmclprl7nxkpj9s1fgiph2quok8894q7f5mkk0 (IDX threeIdKeychain)
        ✔ Name: **3ID Keychain**
        ✔ Schema: ceramic://kjzl6cwe1jw147jz0tc34684e5d8v7p9pmkiivszes02vu9qv7zsb8972xdlbfc (IDX ThreeIdKeychain)
    ✔ kjzl6cwe1jw148j1527vfzj5y064mc46oxboavop92igwxf2yvad502ud6h2oko (IDX basicProfile)
        ✔ Name: **Basic Profile**
        ✔ Schema: ceramic://kjzl6cwe1jw14be7bd6w8go8w0pgveojjrd7bvqrugfdsz6ghzfeo42eqmurd0n (IDX BasicProfile)
    ```

    > This response shows an example of a DID with a 3ID keychain and a basic profile stored in its index.

### View a definition

Use the `idx definition:info` command to view a given definition. If the provided definition is valid it will display the contents of the definition. If it's invalid it will throw an error.

```bash
idx definition:info <DefinitionDocID>
```

=== "Example command"

    ```bash
    idx definition:info kjzl6cwe1jw14blngzz896wlixmclprl7nxkpj9s1fgiph2quok8894q7f5mkk0
    ```

=== "Example response"

    ```bash
    ✔ Definition loaded
    {
    name: '3ID Keychain',
    schema: 'ceramic://kjzl6cwe1jw147jz0tc34684e5d8v7p9pmkiivszes02vu9qv7zsb8972xdlbfc'
    }
    ```

### View a schema

Use the `idx definition:schema` command to view the schema for a given definition:

```bash
idx definition:schema <SchemaDocID>
```

=== "Example command"

    ```bash
    idx definition:schema kjzl6cwe1jw14blngzz896wlixmclprl7nxkpj9s1fgiph2quok8894q7f5mkk0
    ```

=== "Example response"

    ```bash
    ✔ Schema loaded
    {
    type: 'object',
    '$schema': 'http://json-schema.org/draft-07/schema#',
    properties: {
        authMap: {
        type: 'object',
        additionalProperties: { '$ref': '#/definitions/AuthData' }
        },
        pastSeeds: { type: 'array', items: { '$ref': '#/definitions/JWE' } }
    },
    definitions: {
        JWE: {
        type: 'object',
        required: [ 'protected', 'tag', 'ciphertext', 'iv' ],
        properties: {
            iv: { type: 'string' },
            tag: { type: 'string' },
            protected: { type: 'string' },
            ciphertext: { type: 'string' },
            recipients: { type: 'array' }
        }
        },
        AuthData: {
        type: 'object',
        properties: {
            id: { '$ref': '#/definitions/WrappedJWE' },
            pub: { type: 'string' },
            data: { '$ref': '#/definitions/WrappedJWE' }
        },
        additionalProperties: false
        },
        WrappedJWE: {
        type: 'object',
        properties: { jwe: { '$ref': '#/definitions/JWE' } },
        additionalProperties: false
        }
    },
    additionalProperties: false
    }
    ```

## **Inspecting repos**

Use Github or other code collaboration platforms to inspect the repositories of open source projects that use IDX. You will be looking for their JavaScript files which perform [`get`](../../reference/idx.md#get) and [`set`](../../reference/idx.md#set) calls on the IDX API. If they are using [aliases](../../learn/glossary.md#alias), you will see the [definitionIDs](../../learn/glossary.md#definitionid) in their `aliases` object. Otherwise, you will see definitionIDs directly in their calls.

After gathering a list of definitionIDs, follow the steps above to [view a definition](#view-a-definition) and [view a schema](#view-a-schema).

## **Add to your project**

After you have decided which existing definitions you would like to use in your project, add them to the `alias` object in your JavaScript file as shown in [adding aliases](../../build/aliases.md).
