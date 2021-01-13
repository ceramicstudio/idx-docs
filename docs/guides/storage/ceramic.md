# Ceramic storage

Learn how to use [Ceramic documents](../../learn/glossary.md#document) as [external storage](../../learn/glossary.md#external-datastore) for [records](../../learn/glossary.md#record).

!!! example ""
This guide only describes how to use Ceramic documents as external storage for records. If you want to directly store or read content in records then you do not need this guide. See [writing records](../../build/writing.md) or [reading records](../../build/reading.md).

## **Prerequisites**

- [Install the IDX SDK](../../build/installation.md)
- [Add definitions](../../build/aliases.md) that utilize [Ceramic documents](../../learn/glossary.md#document) for [external storage](../../learn/glossary.md#external-datastores) to the `aliases` object in your project's JavaScript file

## **Installation**

Since IDX already depends on [Ceramic](../../learn/glossary.md#ceramic) to store protocol data, you will have it installed in your project. You **do not** need to install any additional software to use Ceramic for external storage.

## **Writing data**

To write data to IDX records and their external Ceramic documents, you must first [authenticate](../../build/authentication.md) the user's DID.

!!! example ""

    For demonstration purposes, we will use the example of a simple note-taking application. This application will store individual notes in Ceramic documents and a list of these notes will be stored in an IDX record. This IDX record will be identified with the `notesList` [alias](../../learn/glossary.md#alias).

### Create a new Ceramic document

Use the `ceramic.createDocument()` method from the [Ceramic API](../../reference/dependency-apis.md#ceramicapi) to create a new note as a Ceramic document:

```javascript
await ceramic.createDocument('tile', { content })
```

TODO: Write how to get the DocID of this note.

### Add the Ceramic document to an IDX record

Use the `idx.set()` method from the [IDX API](../../reference/idx.md) to add the DocID of the note to their `notesList` record.

```js
await idx.set('notesList', '<DocID of Note>')
```

### Update the Ceramic document

Use the `change()` method from the [Document API]() to update the note.

```js
await doc.change({ content })
```

## **Reading data**

### Query the IDX record

Use the `idx.get()` method from the [IDX API](../../reference/idx.md) to query the `notesList` record. In this case it will return a list of DocIDs that represent the notes.

With an authenticated user:

```js
await idx.get('notesList')
```

With an unauthenticated user:

```js
await idx.get('notesList', '<DID>')
```

### Query the Ceramic document

Use the `ceramic.loadDocument()` method from the [Ceramic API](../../reference/dependency-apis.md#ceramicapi) to load a document containing the note. You will need to pass a DocID from the `notesList` record above:

```js
await ceramic.loadDocument('<DocID>')
```

## **More on Ceramic**

For a full description of Ceramic and how to use it, see the [Ceramic documentation](https://developers.ceramic.network).
