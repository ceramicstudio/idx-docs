# Quick start

Get started exploring what's possible with IDX using the [IDX CLI](../reference/cli.md). For runtime usage in your project, you will need to [install the IDX SDK](../reference/idx.md).

!!! example ""

    :octicons-alert-16: IDX is in alpha. Libraries may be unstable and APIs are subject to change. Once [Ceramic Network](https://ceramic.network) launches mainnet in late Q1 2021, IDX will move to production. Data created on IDX during alpha will *not* be portable to production. Please share what you're working on and report any issues in the [IDX Discord](https://chat.idx.xyz).

## **Prerequisites**

The IDX CLI requires [Node.js](https://nodejs.org/en/) v14 and npm v6 (usually installed with Node.js). Make sure to have both installed.

On Linux you will also need the `libsecret` library to be installed, as [instructed here](https://github.com/atom/node-keytar#on-linux).

## **Step 1: Install IDX CLI**

Open your terminal and install the [IDX CLI](../reference/cli.md) and [Ceramic CLI](https://developers.ceramic.network/build/quick-start/#install-the-cli).

```bash
npm install -g @ceramicnetwork/cli @ceramicstudio/idx-cli
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

Let's query a [record](../learn/glossary.md#record) that stores a [basic profile](../guides/definitions/default.md#basic-profile). Use the `idx index:get` command and the `basicProfile` [alias](../learn/glossary.md#alias). As you can see below, we are looking up the profile of user `did:key:z6Mkw1Mpfejq2R76AsQo2qJoAVaF6HH5nLDoHrKrsW5Wdnei`.

=== "Command"

    ```bash
    idx index:get did:key:z6Mkw1Mpfejq2R76AsQo2qJoAVaF6HH5nLDoHrKrsW5Wdnei basicProfile
    ```

=== "Output"

    ```bash
    ✔ Contents successfully loaded
    { name: 'Alan Turing' }
    ```

Since basic profiles are a commonly used definition on IDX, we have assigned it the default `basicProfile` alias for simplicity. [Default definitions](../guides/definitions/default.md) were installed when you ran the `idx bootstrap` command earlier. However, you could run the same `index:get` command using the raw DocID of the basic profile definition instead of its alias and get the same data back.

```bash
idx index:get did:key:z6Mkw1Mpfejq2R76AsQo2qJoAVaF6HH5nLDoHrKrsW5Wdnei kjzl6cwe1jw14bdsytwychcd91fcc7xibfj8bc0r2h3w5wm8t6rt4dtlrotl1ou
```

## **Step 3: Create a DID**

Use the `idx did:create` command to create a new DID enabled with IDX.

=== "Command"

    ```bash
    idx did:create
    ```

=== "Output"

    ```bash
    ✔ Created DID: did:key:z6MkuEd4fm7qNq8hkmWFM1NLVBAXa4t2GcNDdmVzBrRm2DNm
    ```

Use the `idx did:list` command to get your DID from the node.

=== "Command"

    ```bash
    idx did:list
    ```

=== "Output"

    ```bash
    ┌──────────────────────────────────────────────────────────┬────────────┬─────────────────────────────────────────────────────────┐
    │ DID                                                      │ Label      │ Created                                                 │
    ├──────────────────────────────────────────────────────────┼────────────┼─────────────────────────────────────────────────────────┤
    │ did:key:z6MkuEd4fm7qNq8hkmWFM1NLVBAXa4t2GcNDdmVzBrRm2DNm │ (no label) │ Thu Jan 14 2021 11:51:07 GMT+0000 (Greenwich Mean Time) │
    └──────────────────────────────────────────────────────────┴────────────┴─────────────────────────────────────────────────────────┘
    ```

## **Step 4: Create a record**

Use the `idx index:set` command to set data to a [record](../learn/glossary.md#record) for the currently authenticated DID. In this example we're passing the same `basicProfile` alias as above to specify that we want to save data to record corresponding to the default basic profile definition. The final part of this command is the actual contents we want to set to the record. These contents must conform to the schema specified in the definition. If not, the command will fail.

```bash
idx index:set <did:key:myDID> basicProfile '{"name":"YourName"}'
```

## **Step 5: Query your record**

Use the `idx index:get` command to query your newly created basic profile record.

=== "Command"

    ```bash
    idx index:get <did:key:myDID> basicProfile
    ```

=== "Output"

    ```
    The profile that you created in the previoius step
    ```

## **Doing more**

Run the `--h` command to list all commands available in the IDX CLI. All the commands provided by the IDX CLI can also be found in the [CLI documentation](https://github.com/ceramicstudio/js-idx/tree/master/packages/cli#idx-cli).

```bash
idx --help
```

## **That's it!**

Congratulations on completing this introductory tutorial. You're well on your way to becoming an IDX developer.
