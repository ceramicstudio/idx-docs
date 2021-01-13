# Glossary

## Key terms

> Terms and definitions for key protocol components

### **Index**

The index is a key-value store document that stores a list of [definitionID](#definitionid) to [recordID](#recordid) mappings. These mappings repreresent all of the data owned by a given DID. The index is the core component of IDX and each [DID](#did) has only one.

=== "Example index"

    ```json
    {
      "kyz123...456": "kyz789...678",
      "kyz123...456": "kyz789...678",
      "kyz123...456": "kyz789...678",
      "kyz123...456": "kyz789...678"
    }
    ```

### **Definition**

A definition is a document which describes a [record](#record) and its [definitionID](#definitionid) acts as a key in the [index](#index). Definitions contain a [schema](#schema) and other metadata about a record. Definitions are created once by developers and the defiinitionID can be reused as a key in any number of indexes.

=== "Example definition"

    ```js
    {
      name: 'Basic Profile',
      description: 'A simple basic profile.',
      schema: 'kyz...'
    }
    ```

### **Schema**

A schema is a document that contain a [JSON schema](https://json-schema.org/). The [schemaURL](#schemaurl) of the schema is included in a [definition](#definition) and is used to enforce the data format of a [record](#record).

=== "Example schema"

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

### **Record**

A record is a document which contains the JSON data described by a [definition](#definition). The [recordID](#recordid) of the record acts as a value in the [index](#index). Records are unique to users, so different users will have different records for the same definitionID. Records are entirely flexible to your use case, but many developers use them to store content or references to content.

#### Storage

Records can be used to directly store content. Typically, they are used to manage a single JSON object such as a profile or a follow list.

=== "Example storage record"

    ```js
    {
      name: 'Alan Turing',
      description: 'I make computers beep good.',
      emoji: '💻'
    }
    ```

#### References

Records can be used to store references to [external datastores](). Typically these records contain one or more links to a collection of similar files or datastores, such as a list of blog posts or a list of tweets, acting as an entry point to the collection.

=== "Example reference record"

    ```js
    {
      references: ['kyz123...456', 'kyz789...987', 'kyz654...321']
    }
    ```

## Related terms

> Terms and definitions relevant to building with IDX

### **Alias**

An alias is an application-level construct that makes it easy to reference and interact with [definitions](#definition) in your project. Aliases are mappings from human-readable names to [definitionIDs](#definitionid).

=== "Example aliases"

    ```js
    const aliases = {
      alias1: 'definitionID 1',
      alias2: 'definitionID 2',
    }
    ```

### **DID**

DIDs is the [W3C standard](https://www.w3.org/TR/did-core/) for gloablly unique decentralized identifiers. IDX uses DIDs for user identifiers and authentication. There currently are more than 60+ implementations of DIDs, called methods. IDX supports any DID method. Learn more about DIDs in the [Ceramic documentation]().

=== "Example DID"

    ```
    did:3:bafy124123123123123123123123123123
    ```

### **Ceramic**

Ceramic is a decentralized content management network for mutable documents. IDX uses Ceramic to store and query IDX documents including [indexes](#index), [definitions](#definition), [schemas](#schema), and [records](#record).

> Learn more about [Ceramic network]().

### **Document**

A document is a mutable datastore on [Ceramic](#ceramic) that contains verifiable data. Documents are identified by [DocIDs](#docid).

=== "Example Document"

    ```

    ```

### **DocID**

A DocID is a unique, immutable identifier for a [document](#document) on [Ceramic](#ceramic).

=== "Example DocID"

    ```
    kyz4bdj4r8dwb4khf9ep3b4wjrh84qbfbh3477wedoe9fn3fsz9mn
    ```

### **DefinitionID**

A definitionID is a [DocID](#docid) of a [definition](#definition).

### **IndexID**

An indexID is a [docID](#docid) of an [index](#index).

### **SchemaID**

A schemaID is a [docID](#docid) of a [schema](#schema).

### **SchemaURL**

A schemaURL is a [Ceramic]() URL for a [schema](#schema).

### **RecordID**

A recordID is a [docID](#docid) of a [record](#record).

### **VersionID**

### **External datastores**

External datastores are datastores that provide storage for content beyond records. Oftentimes records will contain [references](#references) to one or more external datastores.
