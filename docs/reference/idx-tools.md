# IDX Tools Reference

## Installation

## API Methods

The APIs below are only available in the `idx-tools` library. Additional APIs not found on this page but are also accessible from the `idx-tools` library can be found at [`idx-constants`]().

### **isSecureSchema**

Checks if a JSON schema is valid and secure according to [Ajv's secure schema]().

Arguments:

- `schema`: Schema

Returns: `boolean`

=== "Request"

    ```javascript
    ```

=== "Response"

    ```javascript
    ```

---

### **publishDoc**

Creates or updates a document defined by the PublishDoc interface

Type parameters:

- `T` = unknown

Arguments:

- `ceramic`: CeramicApi
- `doc`: PublishDoc<T>

Returns: `Promise<DocID>`

=== "Request"

    ```javascript
    ```

=== "Response"

    ```javascript
    ```

---

### **createDefinition**

Creates and publishes a new [definition]().

Arguments:

- `ceramic`: CeramicApi
- `definition`: Definition

Returns: `Promise<DocID>`

=== "Request"

    ```javascript
    ```

=== "Response"

    ```javascript
    ```

---

### **updateDefinition**

Similar to [`publishDoc`]() for an existing DefinitionDoc.

Arguments:

- `ceramic`: CeramicApi
- `doc`: DefinitionDoc

Returns: `Promise<boolean>` whether the definition contents have changed

=== "Request"

    ```javascript
    ```

=== "Response"

    ```javascript
    ```

---

### **publishSchema**

Similar to [`publishDoc`]() for a [SchemaDoc](), with additional validation using validateSchema.

Arguments:

- `ceramic`: CeramicApi
- `doc`: SchemaDoc

Returns: `Promise<DocID>`

=== "Request"

    ```javascript
    ```

=== "Response"

    ```javascript
    ```

---

### **publishIDXConfig**

Publishes the signed definitions and schemas provided by IDX.

Arguments:

- `ceramic`: CeramicApi

Returns: `Promise<PublishedConfig>`

=== "Request"

    ```javascript
    ```

=== "Response"

    ```javascript
    ```

</br>
</br>
</br>
