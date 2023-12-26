---
title: Command Line Related Notes
date: 2021-06-05
draft: false
garden_tags: ["en", "notes", "command-line", "cent-os"]
summary: " "
status: "growing"
---

- [1. Switch to end of line in vi:](#1-switch-to-end-of-line-in-vi)
- [2. Switch to end of line in normal command line:](#2-switch-to-end-of-line-in-normal-command-line)
- [3. Switch to specific line in target file:](#3-switch-to-specific-line-in-target-file)
- [4. Look up for filesystems of disk:](#4-look-up-for-filesystems-of-disk)
- [5. Look up for files in disk:](#5-look-up-for-files-in-disk)
- [6. Look up with letter case ignored:](#6-look-up-with-letter-case-ignored)
- [7. Look up for CPU info:](#7-look-up-for-cpu-info)
- [8. Switch to start of line in normal command line:](#8-switch-to-start-of-line-in-normal-command-line)
- [9. Delete one fragment in normal command line:](#9-delete-one-fragment-in-normal-command-line)
- [10. Delete one line in vi:](#10-delete-one-line-in-vi)
- [11. Redo in vi:](#11-redo-in-vi)
- [12. for loop for batch processing](#12-for-loop-for-batch-processing)


# 1. Switch to end of line in vi:

```shell
shift+G
```

# 2. Switch to end of line in normal command line:

```
ctrl+E
```

# 3. Switch to specific line in target file:

```
vi <file directory> +<n>
```

# 4. Look up for filesystems of disk:

```
df -h
```

# 5. Look up for files in disk:

```
du
```

# 6. Look up with letter case ignored:

```
grep -i
```

# 7. Look up for CPU info:

```
htop
```

# 8. Switch to start of line in normal command line:

```
ctrl+A
```

# 9. Delete one fragment in normal command line:

```
ctrl+W
```

# 10. Delete one line in vi:

double click D

# 11. Redo in vi:

double click U

# 12. for loop for batch processing 

```shell
for i in `docker image ls`; do echo "$i"; done
```
