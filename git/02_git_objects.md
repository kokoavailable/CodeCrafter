# Understanding Git Objects

## What Are Git Objects?

Git objects are the foundation of how Git handles version control. They allow Git to efficiently store and retrieve files by computing their unique names from their contents. This makes Git a **content-addressed filesystem**.

Unlike regular filesystems where file names are arbitrary, Git derives file names mathematically from their contents. If the contents of a file change, its internal name (derived from a SHA-1 hash) changes as well. This ensures that files in Git are immutable — any modification creates a new object.

## Low-Level Commands: `git hash-object` and `git cat-file`

Two low-level Git commands related to objects are:

- **`git hash-object`**: Converts an existing file into a Git object.
- **`git cat-file`**: Prints the content of an existing Git object to the standard output.

These commands belong to the "plumbing" category of Git and are not commonly used in everyday workflows.

## Git’s Content-Addressed Storage

Git calculates the SHA-1 hash of a file's contents and uses it as its internal identifier. It then splits this hash into two parts:

1. The first two characters become the directory name.
2. The remaining characters become the file name.

For example, a file with a SHA-1 hash of `29ff16c9c14e2652b22f8b78bb08a5a` would be stored in:

```
.git/objects/29/ff16c9c14e2652b22f8b78bb08a5a
```

This structure ensures that Git avoids filesystem performance issues by evenly distributing objects across directories.

## What Is a Hash Function?

A **hash function** is a mathematical function that computes a fixed-size output (hash) from an input. Properties of hash functions include:

- **Unidirectionality**: It's easy to compute the hash of a value, but impossible to reverse the process.
- **Deterministic**: The same input always produces the same hash.
- **Collision Resistance**: Two different inputs rarely produce the same hash.

Git uses the cryptographic hash function **SHA-1** to compute these hashes.

### Example: The SHA-1 Hash

Consider the classical `len` function, which returns the length of a string. It’s simple to compute the length of "hello" (5), but impossible to determine the original string from just the number 5. SHA-1 operates similarly but on a much more complex level.

## Git Object Structure

Git objects have a specific storage format:

1. **Header**: Specifies the object type (e.g., blob, commit, tag, or tree) and the size of the object in bytes.
2. **Null Separator**: A null byte (0x00) separates the header from the content.
3. **Contents**: The actual data of the object.

### Example Commit Object

The first 48 bytes of a commit object might look like this:

```
00000000  63 6f 6d 6d 69 74 20 31  30 38 36 00 74 72 65 65  |commit 1086.tree|
00000010  20 32 39 66 66 31 36 63  39 63 31 34 65 32 36 35  | 29ff16c9c14e265|
00000020  32 62 32 32 66 38 62 37  38 62 62 30 38 61 35 61  |2b22f8b78bb08a5a|
```

- **Header**: `commit 1086`
- **Null Separator**: `00`
- **Space**: `20`
- **Contents**: Begins with `tree 29ff...`

## Compression with Zlib

To save storage space, Git compresses all objects using **zlib**.

---

By understanding how Git objects work under the hood, you can appreciate the efficiency and robustness of Git's version control system. Whether you’re using Git’s high-level commands or exploring its plumbing, this knowledge forms the foundation for advanced Git operations.

https://wyag.thb.lt/#objects
