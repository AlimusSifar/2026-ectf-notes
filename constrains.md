# Constrains for ECTF Tools commands

> *Legend: \
> Output - Result from command execution \
> Expected - The target result*

## LIST command

`uvx ectf tools <PORT> list <PIN>`

| # | Constrains        | Output   | Expected | Status  |
|---|-------------------|----------|----------|---------|
| 1 | No PIN            | 🟥 ERROR | 🟥 ERROR | ✅ Good |
| 2 | 0 < PIN < 6 Bytes | 🟩 OK    | 🟥 ERROR | ❌ Bad  |
| 3 | PIN > 6 Bytes     | 🟩 OK    | 🟥 ERROR | ❌ Bad  |
| 4 | PIN == 6 Bytes    | 🟩 OK    | 🟩 OK    | ✅ Good |

- PIN validation NOT IMPLEMENTED.

## LISTEN command

The listen tool executes the listen command and returns the result from the HSM.

`ectf tools <PORT> listen`

- Cannot verify if the requested HSM has valid permissions or not.

## WRITE command

`ectf tools <PORT> write [--uuid <UUID>] <PIN> <SLOT> <GID> <FILE_PATH>`

    PIN: text = The pin to authenticate the user
    SLOT: int = The slot to write the file to
    GID: int (base 10/16) = The ID of the group that owns the HSM file
    FILE_PATH: path = The path to a file in the host system
    UUID: text = The UUID of the file (optional, to be firmware generated)

| #  | Constrains            | Output   | Expected | Status  |
|----|-----------------------|----------|----------|---------|
| 1  | No PIN                | 🟥 ERROR | 🟥 ERROR | ✅ Good |
| 2  | 0 < PIN < 6 Bytes     | 🟩 OK    | 🟥 ERROR | ❌ Bad  |
| 3  | PIN > 6 Bytes         | 🟩 OK    | 🟥 ERROR | ❌ Bad  |
| 4  | PIN == 6 Bytes        | 🟩 OK    | 🟩 OK    | ✅ Good |
| 5  | SLOT > 1 Bytes        | ⚠️ TEST  | 🟥 ERROR | ❌ Bad  |
| 6  | SLOT == 1 Bytes       | 🟩 OK    | 🟩 OK    | ✅ Good |
| 7  | 0 < GID < 2 Bytes     | ⚠️ TEST  | 🟥 ERROR | ❌ Bad  |
| 8  | GID > 2 Bytes         | ⚠️ TEST  | 🟥 ERROR | ❌ Bad  |
| 9  | GID == 2 Bytes        | 🟩 OK    | 🟩 OK    | ✅ Good |
| 10 | No FILE_PATH          | ⚠️ TEST  | 🟥 ERROR | ❌ Bad  |
| 11 | FILE_PATH > 32 Bytes  | ⚠️ TEST  | 🟥 ERROR | ❌ Bad  |
| 12 | FILE_PATH <= 32 Bytes | 🟩 OK    | 🟩 OK    | ✅ Good |
| 13 | UUID < 16 Bytes       | ⚠️ TEST  | 🟥 ERROR | ❌ Bad  |
| 14 | UUID > 16 Bytes       | ⚠️ TEST  | 🟥 ERROR | ❌ Bad  |
| 15 | UUID == 16 Bytes      | 🟩 OK    | 🟩 OK    | ✅ Good |

- PIN validation NOT IMPLEMENTED.

## READ command

`ectf tools <PORT> read <PIN> <READ_SLOT> <DIR_PATH>`

| # | Constrains           | Output   | Expected | Status  |
|---|----------------------|----------|----------|---------|
| 1 | No PIN               | 🟥 ERROR | 🟥 ERROR | ✅ Good |
| 2 | 0 < PIN < 6 Bytes    | 🟩 OK    | 🟥 ERROR | ❌ Bad  |
| 3 | PIN > 6 Bytes        | 🟩 OK    | 🟥 ERROR | ❌ Bad  |
| 4 | PIN == 6 Bytes       | 🟩 OK    | 🟩 OK    | ✅ Good |
| 5 | SLOT > 1 Bytes       | ⚠️ TEST  | 🟥 ERROR | ❌ Bad  |
| 6 | SLOT == 1 Bytes      | 🟩 OK    | 🟩 OK    | ✅ Good |
| 7 | No DIR_PATH          | ⚠️ TEST  | 🟥 ERROR | ❌ Bad  |
| 8 | DIR_PATH > 32 Bytes  | ⚠️ TEST  | 🟥 ERROR | ❌ Bad  |
| 9 | DIR_PATH <= 32 Bytes | 🟩 OK    | 🟩 OK    | ✅ Good |

- PIN validation NOT IMPLEMENTED.

## INTERROGATE command

`ectf tools <PORT> interrogate <PIN>`

| # | Constrains        | Output   | Expected | Status  |
|---|-------------------|----------|----------|---------|
| 1 | No PIN            | 🟥 ERROR | 🟥 ERROR | ✅ Good |
| 2 | 0 < PIN < 6 Bytes | 🟩 OK    | 🟥 ERROR | ❌ Bad  |
| 3 | PIN > 6 Bytes     | 🟩 OK    | 🟥 ERROR | ❌ Bad  |
| 4 | PIN == 6 Bytes    | 🟩 OK    | 🟩 OK    | ✅ Good |

- PIN validation NOT IMPLEMENTED.

## Receive command

`ectf tools <PORT> receive <PIN> <READ_SLOT> <WRITE_SLOT>`

| # | Constrains        | Output   | Expected | Status  |
|---|-------------------|----------|----------|---------|
| 1 | No PIN            | 🟥 ERROR | 🟥 ERROR | ✅ Good |
| 2 | 0 < PIN < 6 Bytes | 🟩 OK    | 🟥 ERROR | ❌ Bad  |
| 3 | PIN > 6 Bytes     | 🟩 OK    | 🟥 ERROR | ❌ Bad  |
| 4 | PIN == 6 Bytes    | 🟩 OK    | 🟩 OK    | ✅ Good |
| 5 | No SLOT           | ⚠️ TEST  | 🟥 ERROR | ❌ Bad  |
| 5 | SLOT > 1 Bytes    | ⚠️ TEST  | 🟥 ERROR | ❌ Bad  |
| 6 | SLOT == 1 Bytes   | 🟩 OK    | 🟩 OK    | ✅ Good |

- PIN validation NOT IMPLEMENTED.
- READ_SLOT & WRITE_SLOT validation NOT IMPLEMENTED.
- Receives all the files form the neighbor HSM instead of a single file.
