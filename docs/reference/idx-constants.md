# IDX Constants Reference

## Installation
`idx-constants` is included by default in the [`idx-tools`]() library, but if you wanted to install it separately:

```sh
npm install @ceramicstudio/idx-constants
```

## API Methods

### **schemas**
Returns a record of the schemas included in `idx-constants`, keyed by IDX schema name:

- `BasicProfile`: see [Basic Profile CIP]()
- `CryptoAccounts`: see [Crypto Accounts CIP]()
- `Definition`: (CIP to be defined)
- `IdentityIndex` see [Identity Index CIP]()
- `ThreeIdKeychain`:

Returns: `Record<IDXSchemaName, Schema>`

=== "Request"

    ```javascript
    ```

=== "Response"

    ```javascript
    ```

---

### **signedDefinitions**
Returns a record of signed definitions, keyed by IDX definition [alias]():

Returns: `Record<IDXDefinitionName, DagJWSResult>`

=== "Request"

    ```javascript
    ```

=== "Response"

    ```javascript
    ```

---

### **signedSchemas**
Returns a record of the signed schemas.

Returns: `Record<IDXSchemaName, DagJWSResult>`

=== "Request"

    ```javascript
    ```

=== "Response"

    ```javascript
    ```

</br>
</br>
</br>