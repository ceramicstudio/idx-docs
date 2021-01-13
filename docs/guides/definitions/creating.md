# Creating definitions

If you are not able to only utilize [default definitions](default.md) or [existing definitions](discovering.md), then you will need to create new definitions for your project. Custom definitions allow your application to [write records](../../build/writing.md) and [read records](../../build/reading.md) specifically suited to your use case.

## **Prerequisites**

Make sure you have [installed the CLI](../../reference/cli.md) and that it is running properly. You can use the `command` command to test this. You should see this response:

```bash

```

## **Step 1: Define your records**

Consider your application's data model as a set of discrete [records](../../../learn/glossary/#record). Each record should store a logical subset of information for your project.

```
DID -> Index -> Definition -> Record
					^
				 Schema
```

For demonstration purposes, this guide will use the example of a simple note-taking application that needs to manage a basic profile and a collection of notes. Therefore, this application would use two records:

- A record to store a profile (`basicProfile`)
- A record to store a list of notes (`notesList`)

!!! example ""

    The individual notes objects can be stored in any [external datastore](../../../learn/glossary/#external-datastore), but we will assume these notes are stored in [Ceramic documents](../../../learn/glossary/#document).

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
      $schema: '<http://json-schema.org/draft-07/schema#>',
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
    }
    ```

=== "Example record"

    ```js
    {
      notes: [
        'kyz123...456',
        'kyz123...456',
        'kyz123...456'
      ]
    }
    ```

### Publish your schemas

Use the `schema:publish` command on the IDX CLI to publish each of your schemas. You will need to do this for each of your two schemas above.

```bash
idx schema:publish 'your schema'
```

=== "Example command"

```bash
idx schema:publish 'schema content content content content content content content content'
```

=== "Example response"

```bash
ceramic://k3y52l7qbv1fryd65pd3dyu9dim46vx39z4bgzrrligbi5sfd0e3mwump2p6pdn9c
```

## **Step 3: Create your definitions**

Create [definitions](../../learn/glossary.md#definition) that will act as keys for your records in the index. Definitions include the schema URLs from above and additional metadata.

### Specify your definitions

Because we are using two records in our example, we will need to create two definitions.

#### `basicProfile` definition

```js
'name': 'Profile'
'description': 'A basic user profile'    // optional
'schema': '<schema URL from previous command>'
'config': { }   //optional
```

#### `notesList` definition

```js
'name': 'Notes'
'description': 'A list of notes'    // optional
'schema': '<schema URL from previous command>'
'config': { }   //optional
```

### Publish your definitions

Use the `definition:create` command on the IDX CLI to publish each of your definitions.

```bash
idx definition:create --schema=<schema URL from previous command> --name="definition name" --description="definition description"
```

=== "Example command"

    ```bash
    idx definition:create 'schema content content content content content content content content'
    ```

=== "Example response"

    ```bash
    k3y52l7qbv1fryd65pd3dyu9dim46vx39z4bgzrrligbi5sfd0e3mwump2p6pdn9c
    ```

## **Step 4: Add to your project**

Add the [definitionIDs](../../learn/glossary.md#definitionid) of the definitions that you just created to the `aliases` object in your project's JavaScript file. This will allow you to use them to [read records](../../build/reading.md) and [write records](../../build/writing.md) using the IDX API during runtime.

```js
const aliases = {
	basicProfile: 'k3y52l7qbv1fryd65pd3dyu9dim46vx39z4bgzrrligbi5sfd0e3mwump2p6pdn9c'
	notesList: 'k3y52l7qbv1fryd65pd3dyu9dim46vx39z4bgzrrligbi5sfd0e3mwump2p6pdn9c'
}
```
