# TypeScript types

### **IndexKey**

An opaque key used to identify records in the index.

```ts
type IndexKey = string
```

### **Index**

Represents the shape of the content stored in the index.

```ts
type Index = Record<IndexKey, string>
```

### **Schema**

A type representing a JSON Schema.

```ts
type Schema = Record<string, unknown>
```

### **Definition**

A definition is a Ceramic document that describes a record in the index.

```ts
type Definition<C extends Record<string, any> = Record<string, any>> = {
  name: string
  description: string
  schema: string
  url?: string
  family?: string
  config?: C
}
```

### **DefinitionWithID**

```ts
type DefinitionWithID<
  C extends Record<string, unknown> = Record<string, unknown>
> = Definition<C> & { id: DocID }
```

### **Aliases**

```ts
type Aliases = Record<string, string>
```

### **Entry**

```ts
type Entry = {
  key: IndexKey
  id: string
  record: unknown
}
```

### **DefinitionName**

Name for aliases of core IDX definitions.

```ts
type DefinitionName = 'basicProfile' | 'cryptoAccountLinks' | 'threeIdKeychain'
```

### **PublishedDefinitions**

Record of definitions published to Ceramic.

```ts
type PublishedDefinitions = Record<DefinitionName, string>
```

### **SchemaName**

Name for aliases of core IDX schemas.

```ts
type SchemaName =
  | 'BasicProfile'
  | 'CryptoAccounts'
  | 'Definition'
  | 'IdentityIndex'
  | 'ThreeIdKeychain'
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
