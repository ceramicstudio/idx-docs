# Quick start

Get started exploring what's possible with IDX using the [IDX CLI](../reference/cli.md). For runtime usage in your project, you will need to [install the IDX SDK](../reference/idx.md).

!!! warning ""
:octicons-alert-16: IDX is in alpha. Libraries may be unstable and APIs are subject to change. Please share what you're working on and report any issues in the [IDX Discord](https://chat.idx.xyz).

## **Prerequisites**

The IDX CLI requires [Node.js](https://nodejs.org/en/) and npm (usually installed with Node.js). Make sure to have both installed.

## **Step 1: Install IDX CLI**

Open your terminal and install the [IDX CLI](../reference/cli.md) and [Ceramic CLI]().

```bash
npm install -g @ceramicnetwork/ceramic-cli @ceramicstudio/idx-cli
```

Start the Ceramic daemon. This will start a Ceramic node on your local machine and connect to it on `http://localhost:7007`.

```bash
ceramic daemon
```

Bootstrap IDX on your Ceramic node. This will install certain requirements needed for IDX to properly function.

```bash
idx bootstrap
```

## **Step 2: Query a record**

Let's query an [index](../learn/glossary.md#index) for a [record](../learn/glossary.md#record) that stores a [basic profile](../guides/definitions/default.md#basic-profile). Use the `idx index:get` command and the `basicProfile` [alias](../learn/glossary.md#alias). As you can see below, we are looking up the profile of user `did:3:bafy55555555555555555555555555555555123`.

=== "Command"

    ```bash
    idx index:get <did:3:bafy...123> basicProfile
    ```

=== "Result"

    ```bash
    lorem ipsum
    ```

!!! warning ""
Since basic profiles are a commonly used definition on IDX, we have assigned it the default `basicProfile` alias for simplicity. [Default definitions]() were installed when you ran the `idx bootstrap` command earlier. However, you could run the same `index:get` command using the raw DocID of the basic profile definition instead of its alias and get the same data back.

```bash
idx index:get <did:3:bafy...123> <DocID of basic profile definition>
```

## **Step 3: Create a DID**

Use the `idx did:create` command to create a new DID enabled with IDX.

=== "Command"

    ```bash
    idx did:create
    ```

=== "Example result"

    ```bash
    lorem ipsum
    ```

Use the `idx did:list` command to get your DID from the node.

=== "Command"

    ```bash
    idx did:list
    ```

=== "Example result"

    ```bash
    lorem ipsum
    ```

## **Step 4: Create a record**

Use the `idx index:set` command to set data to a record for the currently authenticated DID. In this example we're passing the same `basicProfile` alias as above to specify that we want to save data to record corresponding to the default basic profile definition. The final part of this command is the actual contents we want to set to the record. These contents must conform to the schema specified in the definition. If not, the command will fail.

```bash
idx index:set <did:3:myDID> basicProfile '{"name":"YourName"}'
```

## **Step 5: Query your record**

Use the `idx index:get` command to query the basic profile record.

=== "Command"

    ```bash
    idx index:get <did:3:myDID> basicProfile
    ```

=== "Example result"

    ```
    The profile that you created in the previoius step
    ```

## **Doing more**

Run the `--h` command to list all commands available in the IDX CLI. All the commands provided by the IDX CLI can also be found in the [CLI documentation]().

```bash
idx --help
```

## **That's it!**

Congratulations on completing this introductory tutorial. You're well on your way to becoming an IDX developer.
