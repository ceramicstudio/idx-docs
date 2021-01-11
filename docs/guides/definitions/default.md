# Default definitions

Default definitions are [definitions]() included in IDX libraries by default. Their [aliases]() can automatically be used to [read records]() and [write records]() without any additional configuration.

!!! example ""
    You **do not** need to add default definitions to your project's `aliases` object.

## **Basic Profile**

The basic profile definition specifies a [record]() which stores a general-purpose, universal profile for a DID. Interact with this record using the `basicProfile` alias.

=== "Definition"

    ```javascript
    ```

    > For more information, see [Basic Profile Definition (CIP-N)]().

=== "Schema"

    ```javascript
    ```

    > For more information, see [Basic Profile Schema (CIP-N)]().

=== "Example record"

    ```javascript
    ```

## **Also Known As**

The Also Known As defintion specifies a [record]() which stores a list of third-party identities that belong to a DID. It is commonly used to store verified social accounts such as Twitter, Github, and Discord. It can also be used to store links to domain names and other public, non-cryptographic identifiers. Interact with this record using the `aka` alias.

=== "Definition"

    ```javascript
    ```

    > For more information, see [Also Known As Definition (CIP-N)]().

=== "Schema"

    ```javascript
    ```

    > For more information, see [Also Known As Schema (CIP-N)]().

=== "Example record"

    ```javascript
    ```

## **Crypto Accounts**

The crypto accounts definition specifies a [record]() which stores a list of cryptographic identities that belong to a DID. Interact with this record using the `cryptoAccounts` alias.

=== "Definition"

    ```javascript
    ```

    > For more information, see [Crypto Accounts Definition (CIP-N)]().

=== "Schema"

    ```javascript
    ```

    > For more information, see [Crypto Accounts Schema (CIP-N)]().

=== "Example record"

    ```javascript
    ```

## **3ID Keychain**

The 3ID keychain definition specifies a [record]() which stores encrypted authentication secrets for a 3ID DID. It allows a 3ID to be authenticated using any number of public key cryptographic accounts and is how DIDs can be authenticated using existing blockchain wallets. Interact with this record using the `threeIdKeychain` alias.

=== "Definition"

    ```javascript
    ```

    > For more information, see [Crypto Accounts Definition (CIP-N)]().

=== "Schema"

    ```javascript
    ```

    > For more information, see [Crypto Accounts Schema (CIP-N)]().

=== "Example record"

    ```javascript
    ```

---

!!! example ""

    **Adding new defaults**

    If you would like to add a new default definition to this list, submit a pull request to [`idx-constants`]() on Github. For your pull request to be accepted:

    - The definition must be captured by a [CIP (Ceramic improvement proposal)]()
    - The schema used in the definition must be captured by a CIP
    - The definition must provide general utility to a large number of IDX applications
</br>
</br>
</br>