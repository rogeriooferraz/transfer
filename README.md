# transfer

## Overview
**`transfer`** - Copy contents and preserve timestamps

A command-line utility to copy contents, from a file or set of files,
to corresponding destination file(s), while preserving the destination
timestamps.

It supports the following use cases:

- from a file to another; or
- from a set of files to another set of files of the same size.

It is useful when you want to **replace files by updated versions**
(e.g. screenshots, pictures, documents) while **keeping their original
time/date metadata**, thus preserving sorting order and history.

## Motivation

When managing collections like screenshots or historical documents,
keeping the correct file modification times is essential for:

- Maintaining **chronological sorting** in file explorers.
- Preserving **historical records** of file edits.
- Avoiding unintended modification dates that confuse workflows.

Manually copying and touching each file is tedious and error-prone.  
This script automates the process with **wildcard pattern support**
and **safe matching**.

## Features
- Supports **wildcards** (globbing) for both source and destination
file groups.
- Ensures **one-to-one correspondence** between source and destination
files.
- **Overwrites** destination file content.
- **Preserves** timestamps (both access and modification times).
- **Safety check**: aborts if the number of files does not match.

## Usage

```
transfer [OPTIONS] source_pattern dest_pattern

ARGUMENTS:
  source_pattern : source file(s) naming pattern
  dest_pattern   : destination file(s) naming pattern

OPTIONS:
  -D, --debug    : Enable debug output
  -h, --help     : Display usage information
  -V, --version  : Show current version
```

### Example

Suppose you have:
- Edited screenshots like
`fixed_Screenshot from 2025-04-27 10-00-00.png`
- Original screenshots like
`Screenshot from 2025-04-27 10-00-00.png`
To update the originals with the fixed versions but
**keep the old timestamps**:

```
transfer "fixed_Screenshot*.png" "Screenshot*.png"
```
This will:
- copy content from `fixed_Screenshot from 2025-04-27 10-00-00.png`
to `Screenshot from 2025-04-27 10-00-00.png`
- preserve date/time attributes of destination file

## Requirements

- Bash or compatible shell

## Testing

Tested on **Ubuntu 24.04** with **GNOME** desktop environment.

## Install

```
cd /tmp
git clone git@github.com:rogeriooferraz/transfer.git
sudo cp transfer/transfer /usr/local/bin/
sudo chmod +x /usr/local/bin/transfer
rm -rf /tmp/transfer
cd -
```

## Uninstall

```
sudo rm /usr/local/bin/transfer
```

## Notes
- Files are matched **by sorted order** (`ls --sort=name`).
- Filenames with spaces are properly handled.
- **The script will abort** if the number of source and destination
files does not match.
- Existing destination files will be
**overwritten without confirmation**.

## License

This project is licensed under the MIT License.<br>
It is free and open source software: you can freely use it, change it, and redistribute it.<br>
There is NO WARRANTY, to the extent permitted by law.

**Project page**: https://github.com/rogeriooferraz/transfer

## Author

Rogerio O. Ferraz (<rogerio.o.ferraz@gmail.com>)
