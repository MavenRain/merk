# merk

Merkle tree state, with LevelUP persistence and a super simple interface.

`merk` uses the ES6 Proxy API to give the best possible interface, it's just an object.
Behind the scenes, `merk` uses a Merkle AVL tree, which lets us do cool things like efficiently iterating through keys, making range proofs, etc. Since every child object is its own tree node, it's fast to update the db and recompute the hash even for very large states.

## Usage

```bash
npm install merk
```

```js
let merk = require('merk')

// creates or loads state
let state = await merk(levelUpDb)

// use state as you would any other object
state.foo = 'bar'
state.baz = { x: 123, y: { z: 456 } }
delete state.baz.x

// save changes and update merkle tree
await merk.commit(state)

// or rollback to last commit
merk.rollback(state)

// get Merkle root hash of last commit
console.log(await merk.rootHash(state))
```

## License

MIT
