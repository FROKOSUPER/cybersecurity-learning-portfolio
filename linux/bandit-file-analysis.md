# Linux File Analysis and Layered Data

## Overview

This lab was inspired by an OverTheWire Bandit exercise involving a hexdump and multiple layers of compressed or archived data. The challenge required more than memorizing commands: each layer had to be identified before choosing the appropriate operation.

This write-up describes the transferable concepts and investigation process. It intentionally omits passwords, flags, exact challenge filenames, and the full solution sequence.

## Learning Objectives

- Explain the difference between a text representation and raw binary data
- Reconstruct binary bytes from a hexdump
- Use shell redirection to save a command's output
- Identify a file based on its contents
- Distinguish compression from archiving
- Process unknown data one verified layer at a time

## 1. Reversing a Hexdump

A hexdump is a text representation of binary data. It makes bytes readable and transferable as characters, but it is not the original binary file.

A generic reconstruction command is:

```bash
xxd -r input.txt > output.bin
```

Here, `xxd -r` reads the hexadecimal representation and recreates the original bytes.

### Why output redirection matters

Running this command without redirection:

```bash
xxd -r input.txt
```

does not replace `input.txt`. The reconstructed bytes are written to standard output, which normally means the terminal. Binary output may therefore appear as unreadable symbols.

The `>` operator redirects standard output into a file:

```text
text hexdump → xxd -r → reconstructed bytes → output file
```

The extension is not what makes the output binary. The bytes stored in the file determine what the file actually contains.

## 2. Identifying the Real File Type

Filenames and extensions can be missing, inaccurate, or intentionally misleading. The `file` command examines characteristics such as magic bytes and structure:

```bash
file output.bin
```

Its result guides the next step. For example, the underlying data might be gzip-compressed, bzip2-compressed, a tar archive, or plain text.

This leads to an important investigation rule:

> Do not assume a file's type from its name. Inspect its contents and verify.

## 3. Compression and Archives

The lab used several formats with different purposes.

### gzip

gzip compresses data. A generic decompression operation is:

```bash
gunzip sample.gz
```

### bzip2

bzip2 is another compression format with a different algorithm:

```bash
bzip2 -d sample.bz2
```

### tar

tar packages one or more files into an archive. It is an archive format, not inherently a compression algorithm:

```bash
tar -xf sample.tar
```

The options mean:

- `-x`: extract files from the archive
- `-f`: use the archive file that follows

Recognizing this difference matters because compressed data must be decompressed, while an archive must be extracted.

## 4. The Iterative Workflow

The central lesson was a repeatable loop:

```text
Identify the current data type
          ↓
Choose the matching operation
          ↓
Process one layer
          ↓
Inspect the new output
          ↓
Repeat until the result is readable
```

A safe generic pattern is:

```bash
file unknown_file
# Select the appropriate tool based on the result.
file new_output
# Continue only after verifying the new format.
```

This avoids guessing and creates a clear chain of evidence for every action.

## Mistakes and Lessons

### Missing a space in a command

Shell commands and their arguments must be separated. For example, `mkdir/path` is interpreted as a command name, while `mkdir /path` runs `mkdir` with `/path` as its argument.

### Checking an old filename after renaming it

After a file is renamed with `mv`, the original name no longer refers to it. Listing the directory with `ls` helps confirm the current state before the next command.

### Using the wrong tar operation

Updating an archive and extracting an archive are different operations. To retrieve its contents, the needed action is extraction with `tar -xf`.

These mistakes were useful because they reinforced a practical habit: read the error, check the current state, correct one assumption, and try again.

## Security Relevance

The same concepts appear in real security work:

- **Digital forensics:** Analysts identify unknown files and unpack evidence without relying on filenames.
- **Malware analysis:** Suspicious programs may be encoded, compressed, or nested to hide their real contents.
- **Incident response:** Responders inspect artifacts methodically and preserve a clear record of each transformation.
- **Data recovery:** Hexadecimal representations can help inspect or reconstruct raw bytes.
- **Threat detection:** File signatures can reveal when content does not match its claimed extension.

The key security mindset is to trust evidence from the data, not assumptions based on appearance.

## What I Learned

The most important lesson was not a single command. It was learning to work through an unfamiliar file systematically:

1. Inspect the evidence.
2. Form a small, testable conclusion about the current format.
3. Use the appropriate tool for one layer.
4. Verify the result before continuing.
5. Document the reasoning without exposing sensitive information.

This workflow is broadly useful in cybersecurity because complex investigations are often solved through a sequence of small, verified steps.

## Next Steps

- Compare magic bytes for several common file formats
- Practice calculating and verifying file hashes
- Learn how permissions and ownership affect evidence handling
- Write a small script that reports file types without automatically extracting untrusted content

## Tools Used

- Linux shell
- `xxd`
- `file`
- `gzip` / `gunzip`
- `bzip2`
- `tar`

## Responsible Disclosure Note

No challenge credentials, secret values, or complete answer sequence are included. This document is a learning reflection, not an answer sheet.
