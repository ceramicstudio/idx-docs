# Creating definitions

If you are not able to only use [default definitions](default.md) or [existing definitions](existing.md), then you will need to create new definitions for your project. Creating new definitions allows your application to [write records](../../build/writing.md) and [read records](../../build/reading.md) specifically suited to your use case.

## **Prerequisites**

Make sure you have [installed the IDX CLI](../cli.md) and that the Ceramic daemon is running properly. You need to be connected to a Ceramic node that you can write to.

## **Step 1: Define your records**

Consider your application's data model as a set of discrete [records](../../learn/glossary.md#record). Each record should store a logical subset of information for your project.

```
DID -> Index -> Definition -> Record
					^
				 Schema
```

For demonstration purposes, this guide will use the example of a simple note-taking application that needs to manage a basic profile and a collection of notes. Therefore, this application would use two records:

- A record to store a profile (`basicProfile`)
- A record to store a list of notes (`notesList`)

!!! example ""

    The individual notes objects can be stored in any [external datastore](../../learn/glossary.md#external-datastore), but we will assume these notes are stored in [Ceramic streams](../../learn/glossary.md#stream). Writing these individual notes will need to be handled by the API of your datastore and is beyond the scope of IDX. An IDX record will just be used to maintain the user's list of notes.

## **Step 2: Create your schemas**

Create JSON schemas to define the data format of your records. All schemas must comply with [JSON schema](https://json-schema.org/) draft 07.

### Specify your schemas

Specify each schema in JSON schema format. Because we are using two records in this example, we will need two schemas.

#### `basicProfile` schema

=== "Schema"

    ```json
    {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "title": "BasicProfile",
      "type": "object",
      "properties": {
        "name": {
          "type": "string",
          "maxLength": 150
        },
        "image": {
          "$ref": "#/definitions/imageSources"
        },
        "description": {
          "type": "string",
          "maxLength": 420
        },
        "emoji": {
          "type": "string",
          "maxLength": 2
        },
        "background": {
          "$ref": "#/definitions/imageSources"
        },
        "birthDate": {
          "type": "string",
          "format": "date",
          "maxLength": 10
        },
        "url": {
          "type": "string",
          "maxLength": 240
        },
        "gender": {
          "type": "string",
          "maxLength": 42
        },
        "homeLocation": {
          "type": "string",
          "maxLength": 140
        },
        "residenceCountry": {
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "maxLength": 2
        },
        "nationalities": {
          "type": "array",
          "minItems": 1,
          "items": {
            "type": "string",
            "pattern": "^[A-Z]{2}$",
            "maxItems": 5
          }
        },
        "affiliations": {
          "type": "array",
          "items": {
            "type": "string",
            "maxLength": 140
          }
        }
      },
      "definitions": {
        "IPFSUrl": {
          "type": "string",
          "pattern": "^ipfs://.+",
          "maxLength": 150
        },
        "positiveInteger": {
          "type": "integer",
          "minimum": 1
        },
        "imageMetadata": {
          "type": "object",
          "properties": {
            "src": {
              "$ref": "#/definitions/IPFSUrl"
            },
            "mimeType": {
              "type": "string",
              "maxLength": 50
            },
            "width": {
              "$ref": "#/definitions/positiveInteger"
            },
            "height": {
              "$ref": "#/definitions/positiveInteger"
            },
            "size": {
              "$ref": "#/definitions/positiveInteger"
            }
          },
          "required": ["src", "mimeType", "width", "height"]
        },
        "imageSources": {
          "type": "object",
          "properties": {
            "original": {
              "$ref": "#/definitions/imageMetadata"
            },
            "alternatives": {
              "type": "array",
              "items": {
                "$ref": "#/definitions/imageMetadata"
              }
            }
          },
          "required": ["original"]
        }
      }
    }
    ```

=== "Example record"

    ```js
    {
      name: 'Alan Turing',
      description: 'I make computers beep good.',
      emoji: '💻'
    }
    ```

#### `notesList` schema

=== "Schema"

    ```js
    {
      $schema: 'http://json-schema.org/draft-07/schema',
      title: 'NotesList',
      type: 'object',
      properties: {
        notes: {
          type: 'array',
          title: 'notes',
          items: {
            type: 'object',
            title: 'NoteItem',
            properties: {
              id: {
                $ref: '#/definitions/CeramicDocId',
              },
              title: {
                type: 'string',
                title: 'title',
                maxLength: 100,
              },
            },
          },
        },
      },
      required: ['notes'],
      definitions: {
        CeramicDocId: {
          type: 'string',
          pattern: '^ceramic://.+(\\?version=.+)?',
          maxLength: 150,
        },
      },
    }
    ```

=== "Example record"

    ```js
    {
      notes: [
        {id: 'kyz123...123'},
        {id: 'kyz123...456'},
        {id: 'kyz123...789'},
      ]
    }
    ```

### Publish your schemas

Use the `schema:publish` command on the IDX CLI to publish each of your schemas. You will need to do this for each of your two schemas above.

```bash
idx schema:publish <DID> 'your schema'
```

=== "Command"

    ```bash
    idx schema:publish did:key:z6MkuEd4fm7qNq8hkmWFM1NLVBAXa4t2GcNDdmVzBrRm2DNm '{"$schema":"http://json-schema.org/draft-07/schema","title":"NotesList","type":"object","properties":{"notes":{"type":"array","title":"notes","items":{"type":"object","title":"NoteItem","properties":{"id":{"$ref":"#/definitions/CeramicDocId"},"title":{"type":"string","title":"title","maxLength":100}}}}},"required":["notes"],"definitions":{"CeramicDocId":{"type":"string","pattern":"^ceramic://.+(\\\\?version=.+)?","maxLength":150}}}'
    ```

=== "Output"

    ```bash
    ✔ Schema published with URL: ceramic://k3y52l7qbv1frxrczisvgwekml7jrdiriv60qrbm80r3uabcl7dqva1rq5rk6b94w
    ```

## **Step 3: Create your definitions**

Create [definitions](../../learn/glossary.md#definition) that will act as keys for your records in the index. Definitions include the schema URLs from above and additional metadata.

### Specify your definitions

Because we are using two records in our example, we will need to create two definitions.

#### `basicProfile` definition

```js
{
  name: 'Profile',
  description: 'A basic user profile', // optional
  schema: '<schema URL from previous command>',
  config: {}, //optional
}
```

#### `notesList` definition

```js
{
  name: 'Notes',
  description: 'A list of notes', // optional
  schema: '<schema URL from previous command>',
  config: {} //optional
}
```

### Publish your definitions

Use the `definition:create` command on the IDX CLI to publish each of your definitions.

```bash
idx definition:create <DID> --schema=<schema URL from previous command> --name="definition name" --description="definition description"
```

=== "Example command"

    ```bash
    idx definition:create did:key:z6MkuEd4fm7qNq8hkmWFM1NLVBAXa4t2GcNDdmVzBrRm2DNm --schema='ceramic://k3y52l7qbv1frxrczisvgwekml7jrdiriv60qrbm80r3uabcl7dqva1rq5rk6b94w' --name="Notes list" --description="A list of notes"
    ```

=== "Example response"

    ```bash
    ✔ Definition successfully created: kjzl6cwe1jw149hunt8wb296aprqjjja96q5etjs2oh97s0t9eku9fuz5or3w1z
    ```

## **Step 4: Add to your project**

Add the [definitionIDs](../../learn/glossary.md#definitionid) of the definitions that you just created to the `aliases` object in your project's JavaScript file. This will allow you to use them to [read records](../../build/reading.md) and [write records](../../build/writing.md) using the IDX API during runtime.

```js
const aliases = {
  basicProfile:
    'kjzl6cwe1jw14bdsytwychcd91fcc7xibfj8bc0r2h3w5wm8t6rt4dtlrotl1ou',
  notesList: 'kjzl6cwe1jw149hunt8wb296aprqjjja96q5etjs2oh97s0t9eku9fuz5or3w1z',
}
```
