# IDX Tools Reference

## Installation

> IDX tools should most likely be installed as a developement dependency, it is not meant to be used at runtime by applications

```sh
npm install -D @ceramicstudio/idx-tools
```

## APIs

### **isValidDefinition()**

Checks if the provided input is a valid [definition](types.md#definition).

**Arguments:**

1. `definition: unknown`

**Returns:** `boolean`

### **isSecureSchema()**

Checks if a JSON schema is valid and secure according to [Ajv's secure schema](https://github.com/ajv-validator/ajv#security-risks-of-trusted-schemas).

**Arguments:**

1. [`schema: Schema`](types.md#schema)

**Returns:** `boolean`

### **publishIDXConfig()**

Publishes the signed definitions and schemas provided by IDX to the provided Ceramic instace.

**Arguments:**

1. [`ceramic: CeramicApi`](dependency-apis.md#ceramicapi)

**Returns:** [`Promise<PublishedConfig>`](types.md#publishedconfig)
