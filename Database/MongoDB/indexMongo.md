## MongoDB indexes use a B-tree data structure.

![B-Tree](./images/index-for-sort.bakedsvg.svg)

## Why do indexes use B-Tree and not Binary Search Tree?

1. B-Tree is a self-balancing tree data structure that maintains sorted data and allows searches, sequential access, insertions, and deletions in logarithmic time.
2. B-Tree is a specialized m-way tree that can be widely used for disk access.
3. B-Tree is optimized for systems that read and write large blocks of data.
4. B-Tree is a self-balancing tree, in which the difference between the height of the left and right subtree for every node is either 0 or 1.
5. B-Tree is a generalization of a binary search tree in that a node can have more than two children.

Reference: [Why do indexes use B-Tree and not Binary Search Tree?](https://www.mongodb.com/community/forums/t/why-do-indexes-use-b-tree-and-not-binary-search-tree/7357)

## syntax

1. Create an index on a field

```js
db.collection.createIndex( { field: <type> } )
```

Example:

```js
db.collection.createIndex({ name: 1 });
```

2. Create a unique index on a field

```js
db.collection.createIndex( { field: <type> }, { unique: true } )
```

3. Create a compound index on two fields

```js
db.collection.createIndex( { field1: <type>, field2: <type> } )
```

Note: cannot index parallel arrays.

## What means isMultiKey in explain()?

1. isMultiKey: true means that the index is a multikey index.
2. isMultiKey: false means that the index is not a multikey index.

## Prefix rules

1. The index prefix is the beginning subset of the index key pattern.

Example:

```js
db.collection.createIndex({ a: 1, b: 1, c: 1 });
```

Find query can use index:

```js
db.collection.find({ a: 'a', b: 'b', c: 'c' });

db.collection.find({ a: 'a', c: 'c' });

db.collection.find({ a: 'a' });

db.collection.find({});
```

Cannot use index:

```js
db.collection.find({ b: 'b', c: 'c' });
```

Explain vietnamese: quy tắc tiền tố khi dùng index, các câu query có thể dùng index khi có field đầu tiên trong index, các field sau không cần phải có.
