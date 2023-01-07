# KVBase

KVBase is a lightweight key-value store for Bun. It internally uses `bun:sqlite` for the storage.

# Lilo's Modification

[Lilo](https://github.com/LiloLookup/Lilo) is a quick Minecraft server lookup and statistics provider and as such a
service relies on performance and stability, we've decided to switch over to [bun](https://bun.sh) and use
this modified [kvb](https://github.com/gaurishhs/kvb) fork as a easy to use and maintain database.

*But what does this fork modify?*
<br>
Well, it mainly modifies the syntax in order to keep it very similar
to [node-redis](https://github.com/redis/node-redis) & to expand [kvb](https://github.com/gaurishhs/kvb)'s capabilities.

Thank you [gaurishhs](https://github.com/gaurishhs) for providing the base of [kvb](https://github.com/gaurishhs/kvb) ❤️

## Installation

```sh
git submodule add https://github.com/LiloLookup/kvb
```

## Usage

> **Warning**: Usage might modify over the next time without a proper documentation. We will promise to update the
> documentation once we're comfortable about the end-result.

```ts
import {KVBase} from 'kvb';

const db = new KVBase();

await db.set('foo', 'bar');
await db.get('foo'); // bar
await db.delete('foo');
await db.update('foo', 'bar');
```

> **Note:** If no `options.bunOptions.filename` is given, Memory Storage will be used.

## Typescript Support

KVBase is written in Typescript and has full types support.

Use Typescript Generics while creating a new instance of KVBase to get the correct types.

```ts
import {KVBase} from 'kvb';

const db = new KVBase<string>();

await db.set('foo', 'bar');
await db.get('foo'); // bar
```

## API

### `new KVBase(options: KVBaseOptions)`

Creates a new instance of KVBase.

#### `options`

Type: `KVBaseOptions`
Source: `src/index.ts`

```ts
interface KVBaseOptions {
    /**
     * Bun options given to the bun:sqlite instance.
     */
    bunOptions?: {
        filename?: string;
        options?: number | { readonly?: boolean; create?: boolean; readwrite?: boolean; }
    };
    /**
     * The name of the table to use.
     * @Default 'kvbase'
     */
    tableName?: string;
}
```

### `db.set(key: string, value: any)`

Sets a key-value pair in the database.

### `db.get(key: string)`

Gets a value from the database.

### `db.delete(key: string)`

Deletes a key-value pair from the database.

### `db.update(key: string, value: any)`

Updates a key-value pair in the database.

### `db.close()`

Close the database connection.

## License

MIT © [Gaurish Sethia](https://gaurishsethia.me). See [LICENSE](https://github.com/gaurishhs/kvb/tree/main/LICENSE) for
more details.