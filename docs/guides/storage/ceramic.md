# Ceramic storage

Learn how to use [Ceramic streams](../../learn/glossary.md#stream) as [external storage](../../learn/glossary.md#external-datastore) for [records](../../learn/glossary.md#record).

!!! example ""
This guide only describes how to use Ceramic streams as external storage for records. If you want to directly store or read content in records then you do not need this guide. See [writing records](../../build/writing.md) or [reading records](../../build/reading.md).

## **Prerequisites**

- [Install the IDX SDK](../../build/installation.md)
- [Add definitions](../../build/aliases.md) that utilize [Ceramic streams](../../learn/glossary.md#stream) for [external storage](../../learn/glossary.md#external-datastores) to the `aliases` object in your project's JavaScript file

## **Installation**

Since IDX already depends on [Ceramic](../../learn/glossary.md#ceramic) to store protocol data, you will have it installed in your project. You **do not** need to install any additional software to use Ceramic for external storage.

## **Writing data**

To write data to IDX records and their external Ceramic streams, you must first [authenticate](../../build/authentication.md) the user's DID.

!!! example ""

    For demonstration purposes, we will use [this example of a simple note-taking application](https://blog.ceramic.network/how-to-build-a-simple-notes-app-with-idx/). This application will store individual notes in Ceramic streams and a list of these notes will be stored in an IDX record. This IDX record will be identified with the `notesList` [alias](../../learn/glossary.md#alias) and use the described [data model](https://blog.ceramic.network/how-to-build-a-simple-notes-app-with-idx/#data-model).

### Create a new Ceramic stream

Use the [`TileDocument.create()` static method](https://developers.ceramic.network/reference/typescript/classes/_ceramicnetwork_stream_tile.tiledocument-1.html#create) from `@ceramicnetwork/stream-tile` to create a new note as a Ceramic stream:

```javascript
const stream = await TileDocument.create(ceramic, {
  date: new Date().toISOString(),
  text: 'Hello world',
})
```

### Add the Ceramic stream to an IDX record

Use the `idx.set()` method from the [IDX API](../../reference/idx.md) to add the StreamID of the note to their `notesList` record.

```js
await idx.set('notesList', {
  notes: [{ id: stream.id.toUrl(), title: 'My first note' }],
})
```

### Update the Ceramic stream

Use the [`update()` method](https://developers.ceramic.network/reference/typescript/classes/_ceramicnetwork_stream_tile.tiledocument-1.html#update) of the `TileDocument` instance to update the note.

```js
await stream.update({ date: stream.content.date, text: 'Hello Ceramic' })
```

## **Reading data**

### Query the IDX record

Use the `idx.get()` method from the [IDX API](../../reference/idx.md) to query the `notesList` record. In this case it will return a list of StreamIDs that represent the notes.

With an authenticated user:

```js
await idx.get('notesList')
```

With an unauthenticated user:

```js
await idx.get('notesList', '<DID>')
```

### Query the Ceramic stream

Use the [`TileDocument.load()` static method](https://developers.ceramic.network/reference/typescript/classes/_ceramicnetwork_stream_tile.tiledocument-1.html#load) from the `@ceramicnetwork/stream-tile` to load a stream containing the note. You will need to pass a StreamID from the `notesList` record above:

```js
await TileDocument.load(ceramic, '<StreamID>')
```

## **More on Ceramic**

For a full description of Ceramic and how to use it, see the [Ceramic documentation](https://developers.ceramic.network).
