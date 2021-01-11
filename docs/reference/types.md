# TypeScript types

### **IndexKey**

An opaque key used to identify records in the index.

```ts
type IndexKey = string
```

### **Schema**

A type representing a JSON Schema.

```ts
type Schema = Record<string, unknown>
```

### **Definition**

A definition is a Ceramic document that describes a record in the index.

```ts
interface Definition<T = unknown> {
  name: string
  schema: string
  description: string
  url?: string
  family?: string
  config?: T
}
```

### **DefinitionsAliases**

```ts
type DefinitionsAliases = Record<string, string>
```

### **ContentEntry**

```ts
interface ContentEntry {
  key: IndexKey
  ref: string
  content: unknown
}
```

### **IdentityIndexContent**

Represents the shape of the content stored in the index.

```ts
type IdentityIndexContent = Record<IndexKey, string>
```

### **EncodedDagJWS**

```ts
interface EncodedDagJWS {
  payload: string
  signatures: Array<JWSSignature>
  link: string
}
```

### **EncodedDagJWSResult**

```ts
interface EncodedDagJWSResult {
  jws: EncodedDagJWS
  linkedBlock: string
}
```

### **DefinitionName**

Name aliases of definitions provided by the [`idx-tools`]() library.

```ts
type DefinitionName = 'basicProfile' | 'cryptoAccountLinks' | 'threeIdKeychain'
```

### **SignedDefinitions**

Signed definitions provided by the [`idx-tools`]() library.

```ts
type SignedDefinitions = Record<DefinitionName, DagJWSResult>
```

### **PublishedDefinitions**

Record of definitions published to Ceramic.

```ts
type PublishedDefinitions = Record<DefinitionName, string>
```

### **SchemaName**

Names of schemas provided by the [`idx-tools`]() library

```ts
type SchemaName =
  | 'BasicProfile'
  | 'CryptoAccounts'
  | 'Definition'
  | 'IdentityIndex'
  | 'ThreeIdKeychain'
```

### **SignedSchemas**

Signed schemas provided by the [`idx-tools`]() library

```ts
type SignedSchemas = Record<SchemaName, DagJWSResult>
```

### **PublishedSchemas**

Record of schemas published to Ceramic.

```ts
type PublishedSchemas = Record<SchemaName, string>
```

### **PublishedConfig**

Definitions and schemas published to Ceramic.

```ts
interface PublishedConfig {
  definitions: PublishedDefinitions
  schemas: PublishedSchemas
}
```

### **PublishDoc**

```ts
interface PublishDoc<T = unknown> {
  id?: DocID | string
  content: T
  controllers?: Array<string>
  schema?: DocID | string
}
```

### **DefinitionDoc**

```ts
interface DefinitionDoc extends PublishDoc<Definition> {
  id: DocID | string
}
```

### **SchemaDoc**

```ts
interface SchemaDoc extends PublishDoc<Schema> {
  name: string
}
```

### **IDXOptions**

Options used by the IDX class constructor

```ts
interface IDXOptions {
  aliases?: DefinitionsAliases
  autopin?: boolean
  ceramic: CeramicApi
}
```

### **CreateOptions**

Options used by the [`.set`]() method of the IDX class.

```ts
interface CreateOptions {
  pin?: boolean
}
```
