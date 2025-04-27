# transfer

## Overview
**`transfer`** is a command-line utility to copy contents, from
a source to a destination, while preserving the destination timestamps.

It supports the following use cases:

- from a file to another; or
- from a set of files to another set of files of the same size.

It is useful when you want to **replace files by updated versions**
(e.g. screenshots, pictures, documents) while **keeping their original
time/date metadata**, thus preserving sorting order and history.

---

## Motivation

When managing collections like screenshots or historical documents,
keeping the correct file modification times is essential for:

- Maintaining **chronological sorting** in file explorers.
- Preserving **historical records** of file edits.
- Avoiding unintended modification dates that confuse workflows.

Manually copying and touching each file is tedious and error-prone.  
This script automates the process with **wildcard pattern support**
and **safe matching**.

---

## Features
- Supports **wildcards** (globbing) for both source and destination
file groups.
- Ensures **one-to-one correspondence** between source and destination
files.
- **Overwrites** destination file content.
- **Preserves** timestamps (both access and modification times).
- **Safety check**: aborts if the number of files does not match.

---

## Installation on Linux

```bash
cd /tmp
git clone git@github.com:rogeriooferraz/transfer.git
sudo cp transfer/transfer /usr/local/bin/
sudo chmod +x /usr/local/bin/transfer
```

---

## Usage

```bash
./transfer "source_pattern" "destination_pattern"
```

### Parameters
- **`source_pattern`**: Wildcard pattern for files providing
**new content**.
- **`destination_pattern`**: Wildcard pattern for files to
**receive content** (timestamps will be preserved).

### Example

Suppose you have:
- Edited screenshots like
`fixed_Screenshot from 2025-04-27 10-00-00.png`
- Original screenshots like
`Screenshot from 2025-04-27 10-00-00.png`
To update the originals with the fixed versions but
**keep the old timestamps**:

```bash
./transfer "fixed_Screenshot*.png" "Screenshot*.png"
```
This will:
- Copy content from `fixed_Screenshot from 2025-04-27 10-00-00.png`
to `Screenshot from 2025-04-27 10-00-00.png`
- Preserve the original timestamp of the destination file

---

## Requirements

- Bash shell
- Standard GNU utilities (`cp`, `touch`, `ls`, `paste`)

Tested on **Ubuntu 24.04** with **GNOME + X11** environment.

---

## Notes
- Files are matched **by sorted order** (`ls --sort=name`).
- Filenames with spaces are properly handled.
- **The script will abort** if the number of source and destination
files does not match.
- Existing destination files will be
**overwritten without confirmation**.

---

## License

MIT License — free to use, modify, and distribute.
