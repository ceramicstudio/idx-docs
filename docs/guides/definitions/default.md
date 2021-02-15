# Default definitions

Default definitions are [definitions](../../learn/glossary.md#definition) included in IDX libraries by default. Their [aliases](../../learn/glossary.md#alias) can automatically be used to [read records](../../build/reading.md) and [write records](../../build/writing.md) without any additional configuration.

!!! example ""

    You **do not** need to add default definitions to your project's `aliases` object.

## **Basic Profile**

The basic profile definition specifies a [record](../../learn/glossary.md#record) which stores a general-purpose, universal profile for a DID. Interact with this record using the `basicProfile` alias.

=== "Definition"

    ```js
    {
      name: 'Basic Profile',
      description: 'Basic profile information for a DID',
      schema: 'ceramic://k3y52l7qbv1frxjdr9qpn9ldvbxb0jg4eig7wtjkdu6gk84vyazw9j4txf4o6d2io',
    }
    ```

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

> For more information, see [Basic Profile Definition (CIP-19)](https://github.com/ceramicnetwork/CIP/blob/master/CIPs/CIP-19/CIP-19.md).

<!--
## **Also Known As**

The Also Known As defintion specifies a [record](../../learn/glossary.md#record) which stores a list of third-party identities that belong to a DID. It is commonly used to store verified social accounts such as Twitter, Github, and Discord. It can also be used to store links to domain names and other public, non-cryptographic identifiers. Interact with this record using the `aka` alias.

=== "Definition"

    ```js
    ```

=== "Schema"

    ```json
    ```

=== "Example record"

    ```js
    ```

> For more information, see [Crypto Accounts Definition (CIP-21)](https://github.com/ceramicnetwork/CIP/blob/master/CIPs/CIP-21/CIP-21.md).
-->

## **Crypto Accounts**

The crypto accounts definition specifies a [record](../../learn/glossary.md#record) which stores a list of cryptographic identities that belong to a DID. Interact with this record using the `cryptoAccounts` alias.

=== "Definition"

    ```js
    {
      name: 'Crypto Accounts',
      description: 'Crypto accounts linked to your DID',
      schema: 'ceramic://k3y52l7qbv1fry6z45y9s2w5npe0nyokbp0oiv1tdhvswhv07lb2v13zdz4i1bp4w',
    }
    ```

=== "Schema"

    ```json
    {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "type": "object",
      "title": "CryptoAccountLinks",
      "patternProperties": {
        "^[a-zA-Z0-9]{1,63}@[-a-zA-Z0-9]{3,16}:[-a-zA-Z0-9]{1,47}": {
          "type": "string",
          "pattern": "^ceramic://.+",
          "maxLength": 1024
        }
      },
      "propertyNames": {
        "maxLength": 1024
      },
      "additionalProperties": false
    }
    ```

=== "Example record"

    ```js
    {
        '0x123@eip155:1': 'ceramic://kjz123...456',            // Ethereum acct and proof
        '0x123@polkadot:b0a...70f': 'ceramic://kjz987...654',  // Polkadot acct and proof
        '0x123@fil:f': 'ceramic://kjz528...912',               // Filecoin acct and proof
        '0x134@cosmos:cosmoshub-2': 'ceramic://kjz382...565'   // Cosmos acct and proof
    }
    ```

## **3ID Keychain**

The 3ID keychain definition specifies a [record](../../learn/glossary.md#record) which stores encrypted authentication secrets for a 3ID DID. It allows a 3ID to be authenticated using any number of public key cryptographic accounts and is how DIDs can be authenticated using existing blockchain wallets. Interact with this record using the `threeIdKeychain` alias.

=== "Definition"

    ```js
    {
      name: '3ID Keychain',
      description: 'Key data for 3ID',
      schema: 'ceramic://k3y52l7qbv1fry69sodu0hc4nwvzglaxxvy3l0xdw7v1o36gyu2dl9us472qh8veo',
    }
    ```

=== "Schema"

    ```json
    {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "definitions": {
        "JWE": {
          "title": "JWE",
          "type": "object",
          "properties": {
            "protected": { "type": "string" },
            "iv": { "type": "string" },
            "ciphertext": { "type": "string" },
            "tag": { "type": "string" },
            "aad": { "type": "string" },
            "recipients": {
              "type": "array",
              "items": {
                "type": "object",
                "properties": {
                  "header": { "type": "object" },
                  "encrypted_key": { "type": "string" }
                },
                "required": ["header", "encrypted_key"]
              }
            }
          },
          "required": ["protected", "iv", "ciphertext", "tag"]
        },
        "WrappedJWE": {
          "type": "object",
          "additionalProperties": false,
          "properties": {
            "jwe": {
              "$ref": "#/definitions/JWE"
            }
          }
        },
        "AuthData": {
          "type": "object",
          "additionalProperties": false,
          "properties": {
            "id": {
              "$ref": "#/definitions/WrappedJWE"
            },
            "pub": {
              "type": "string"
            },
            "data": {
              "$ref": "#/definitions/WrappedJWE"
            }
          }
        }
      },
      "type": "object",
      "additionalProperties": false,
      "properties": {
        "authMap": {
          "type": "object",
          "additionalProperties": {
            "$ref": "#/definitions/AuthData"
          }
        },
        "pastSeeds": {
          "type": "array",
          "items": {
            "$ref": "#/definitions/JWE"
          }
        }
      }
    }
    ```

=== "Example record"

    ```js
    ```

<!-- > For more information, see [3ID Keychain Definition (CIP-N)](). -->

---

!!! example ""

    **Adding new defaults**

    If you would like to add a new default definition to this list, submit a pull request to [`idx-constants`](https://github.com/ceramicstudio/js-idx/tree/master/packages/constants) on Github. For your pull request to be accepted:

    - The definition must be captured by a [CIP (Ceramic improvement proposal)](https://github.com/ceramicnetwork/CIP)
    - The schema used in the definition must be captured by a CIP
    - The definition must provide general utility to a large number of IDX applications
