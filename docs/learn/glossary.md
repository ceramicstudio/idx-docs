# Glossary

## Key terms

> Terms and definitions for key protocol components

### **Index**

The index is a key-value store stream that stores a list of [definitionID](#definitionid) to [recordID](#recordid) mappings. These mappings represent all of the data owned by a given DID. The index is the core component of IDX and each [DID](#did) has only one.

=== "Example index"

    ```json
    {
      "kyz123...456": "ceramic://kyz789...012",
      "kyz345...678": "ceramic://kyz901...234",
      "kyz567...890": "ceramic://kyz123...456",
      "kyz789...012": "ceramic://kyz345...678"
    }
    ```

### **Definition**

A definition is a stream which describes a [record](#record) and its [definitionID](#definitionid) acts as a key in the [index](#index). Definitions contain a [schema](#schema) and other metadata about a record. Definitions are created once by developers and the [definitionID](#definitionid) can be reused as a key in any number of indexes.

=== "Example definition"

    ```js
    {
      name: 'Basic Profile',
      description: 'A simple basic profile.',
      schema: 'ceramic://kyz...'
    }
    ```

### **Schema**

A schema is a stream that contains a [JSON schema](https://json-schema.org/). The [schemaURL](#schemaurl) of the schema is included in a [definition](#definition) and is used to enforce the data format of a [record](#record).

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

A record is a stream which contains the JSON data described by a [definition](#definition). The [recordID](#recordid) of the record acts as a value in the [index](#index). Records are unique to users, so different users will have different records for the same [definitionID](#definitionid). Records are entirely flexible to your use case, but many developers use them to store content or references to content.

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

Records can be used to store references to [external datastores](#external-datastores). Typically these records contain one or more links to a collection of similar files or datastores, such as a list of blog posts or a list of tweets, acting as an entry point to the collection.

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

DIDs is the [W3C standard](https://www.w3.org/TR/did-core/) for globally unique decentralized identifiers. IDX uses DIDs for user identifiers and authentication. There currently are more than 60+ implementations of DIDs, called methods. IDX supports any DID method. Learn more about DIDs in the [Ceramic documentation](https://developers.ceramic.network).

=== "Example DID"

    ```
    did:3:bafy124123123123123123123123123123
    ```

### **CAIP-10 Account ID**

[CAIP-10 Account IDs](https://github.com/ChainAgnostic/CAIPs/blob/master/CAIPs/caip-10.md) is a blockchain agnostic way to describe an account on any blockchain. This may be an externally owned key-pair account, or a smart contract account. IDX uses CAIP-10s as a way to lookup the DID of a user using a `caip10-link` streamType in Ceramic. Learn more in the [Ceramic documentation](https://developers.ceramic.network).

=== "Example CAIP-10 Account IDs"

    ```
    # Ethereum mainnet
    0xab16a96d359ec26a11e2c2b3d8f8b8942d5bfcdb@eip155:1

    # Bitcoin mainnet
    128Lkh3S7CkDTBZ8W7BbpsN3YYizJMp8p6@bip122:000000000019d6689c085ae165831e93

    # Cosmos Hub
    cosmos1t2uflqwqe0fsj0shcfkrvpukewcw40yjj6hdc0@cosmos:cosmoshub-3

    # Kusama network
    5hmuyxw9xdgbpptgypokw4thfyoe3ryenebr381z9iaegmfy@polkadot:b0a8d493285c2df73290dfb7e61f870f
    ```

### **Ceramic**

Ceramic is a decentralized content management network for mutable data streams. IDX uses Ceramic to store and query IDX streams including [indexes](#index), [definitions](#definition), [schemas](#schema), and [records](#record).

> Learn more about [Ceramic network](https://developers.ceramic.network).

### **Stream**

A stream is a mutable datastore on [Ceramic](#ceramic) that contains verifiable data. Streams are identified by [StreamIDs](#streamid).

### **StreamID**

A StreamID is a unique, immutable identifier for a [stream](#stream) on [Ceramic](#ceramic).

=== "Example StreamID"

    ```
    kyz4bdj4r8dwb4khf9ep3b4wjrh84qbfbh3477wedoe9fn3fsz9mn
    ```

### **DefinitionID**

A definitionID is a [StreamID](#streamid) of a [definition](#definition).

### **IndexID**

An indexID is a [StreamID](#streamid) of an [index](#index).

### **SchemaID**

A schemaID is a [StreamID](#streamid) of a [schema](#schema).

### **SchemaURL**

A schemaURL is a [Ceramic](#ceramic) URL for a [schema](#schema).

### **RecordID**

A recordID is a [StreamID](#streamid) of a [record](#record).

### **External datastores**

External datastores are datastores that provide storage for content beyond records. Oftentimes records will contain [references](#references) to one or more external datastores.
