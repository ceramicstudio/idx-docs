# Existing definitions

When deciding which [definitions](../../learn/glossary.md#definition) to use in your project, you might consider utilizing existing definitions. Existing definitions allow your application to [read records](../../build/reading.md) and [write records](../../build/writing.md) originally created by another application. This enables simple cross-application data sharing.

## **Ways to discover definitions**

There are two primary mechanisms for discovering existing definitions:

- [Inspect the indexes](#inspecting-indexes) of known DIDs to see which definitions they have
- [Inspect the Github repos](#inspecting-repositories) of open source projects to see which definitions they're using

## **Inspecting indexes**

Use the [IDX CLI](../../reference/cli.md) to inspect the [indexes](../../learn/glossary.md#index) of known DIDs.

### Prerequisites

- You must have a properly configured IDX CLI. See [using the CLI](../../guides/cli.md) to get started.
- You must have a list of known DIDs that are relevant to your application, such as existing users or target users. You can get creative assembling this list using any means available to you. It's worth noting that many 3ID DIDs have blockchain accounts publicly linked to their DID, which can be used to lookup their DID from their blockchain account.

### List all definitions

Use the `idx index:inspect` command to view all definitions for a given DID:

```bash
idx index:inspect <UserDID>
```

=== "Command"

    ```bash
    idx index:inspect did:key:z6MkuEd4fm7qNq8hkmWFM1NLVBAXa4t2GcNDdmVzBrRm2DNm
    ```

=== "Output"

    ```bash
    ✔ IDX document loaded
      ✔ kjzl6cwe1jw14bdsytwychcd91fcc7xibfj8bc0r2h3w5wm8t6rt4dtlrotl1ou (IDX basicProfile)
        ✔ Definition: Basic Profile (Basic profile information for a DID)
        ✔ Schema: ceramic://k3y52l7qbv1frxjdr9qpn9ldvbxb0jg4eig7wtjkdu6gk84vyazw9j4txf4o6d2io (IDX BasicProfile)
    ```

    > This response shows an example of a DID with a basic profile stored in its index.

### View a definition

Use the `idx definition:info` command to view a given definition. If the provided definition is valid it will display the contents of the definition. If it's invalid it will throw an error.

```bash
idx definition:info <DefinitionDocID>
```

=== "Command"

    ```bash
    idx definition:info kjzl6cwe1jw14bdsytwychcd91fcc7xibfj8bc0r2h3w5wm8t6rt4dtlrotl1ou
    ```

=== "Output"

    ```bash
    ✔ Definition loaded
    {
      name: 'Basic Profile',
      schema: 'ceramic://k3y52l7qbv1frxjdr9qpn9ldvbxb0jg4eig7wtjkdu6gk84vyazw9j4txf4o6d2io',
      description: 'Basic profile information for a DID',
      id: DocID(kjzl6cwe1jw14bdsytwychcd91fcc7xibfj8bc0r2h3w5wm8t6rt4dtlrotl1ou)
    }
    ```

### View a schema

Use the `idx definition:schema` command to view the schema for a given definition:

```bash
idx definition:schema <SchemaDocID>
```

=== "Command"

    ```bash
    idx definition:schema kjzl6cwe1jw14blngzz896wlixmclprl7nxkpj9s1fgiph2quok8894q7f5mkk0
    ```

=== "Output"

    ```bash
    ✔ Schema loaded
    {
      type: 'object',
      title: 'BasicProfile',
      '$schema': 'http://json-schema.org/draft-07/schema#',
      properties: {
        url: { type: 'string', maxLength: 240 },
        name: { type: 'string', maxLength: 150 },
        emoji: { type: 'string', maxLength: 2 },
        image: { '$ref': '#/definitions/imageSources' },
        gender: { type: 'string', maxLength: 42 },
        birthDate: { type: 'string', format: 'date', maxLength: 10 },
        background: { '$ref': '#/definitions/imageSources' },
        description: { type: 'string', maxLength: 420 },
        affiliations: { type: 'array', items: { type: 'string', maxLength: 140 } },
        homeLocation: { type: 'string', maxLength: 140 },
        nationalities: {
          type: 'array',
          items: { type: 'string', pattern: '^[A-Z]{2}$', maxItems: 5 },
          minItems: 1
        },
        residenceCountry: { type: 'string', pattern: '^[A-Z]{2}$', maxLength: 2 }
      },
      definitions: {
        IPFSUrl: { type: 'string', pattern: '^ipfs://.+', maxLength: 150 },
        imageSources: {
          type: 'object',
          required: [ 'original' ],
          properties: {
            original: { '$ref': '#/definitions/imageMetadata' },
            alternatives: {
              type: 'array',
              items: { '$ref': '#/definitions/imageMetadata' }
            }
          }
        },
        imageMetadata: {
          type: 'object',
          required: [ 'src', 'mimeType', 'width', 'height' ],
          properties: {
            src: { '$ref': '#/definitions/IPFSUrl' },
            size: { '$ref': '#/definitions/positiveInteger' },
            width: { '$ref': '#/definitions/positiveInteger' },
            height: { '$ref': '#/definitions/positiveInteger' },
            mimeType: { type: 'string', maxLength: 50 }
          }
        },
        positiveInteger: { type: 'integer', minimum: 1 }
      }
    }
    ```

## **Inspecting repositories**

Use Github or other code collaboration platforms to inspect the repositories of open source projects that use IDX. To locate these projects, you can either view the [ecosystem page](../../learn/ecosystem.md) or lookup the Github topics for [#idx](https://github.com/topics/idx) and [#identityindex](https://github.com/topics/identityindex). Once you find a set of projects, you will be looking for their JavaScript files which perform [`get`](../../reference/idx.md#get) and [`set`](../../reference/idx.md#set) calls on the IDX API. If they are using [aliases](../../learn/glossary.md#alias), you will see the [definitionIDs](../../learn/glossary.md#definitionid) in their `aliases` object. Otherwise, you will see definitionIDs directly in their calls.

After gathering a list of definitionIDs, follow the steps above to [view a definition](#view-a-definition) and [view a schema](#view-a-schema).

## **Add to your project**

After you have decided which existing definitions you would like to use in your project, add them to the `alias` object in your JavaScript file as shown in [adding aliases](../../build/aliases.md).
