---
title: Command Line Related Notes
date: 2021-06-05 00:31:29
<<<<<<< HEAD
categories: 
- Notes
tags:
- Cent OS
- Command Line
- en
=======
categories:
- Notes
- En
tags:
- Cent OS
- Command Line
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
---

#### 1. Switch to end of line in vi:

<<<<<<< HEAD
```shell
shift+G
```

#### 2. Switch to end of line in normal command line:

```
ctrl+E
```

#### 3. Switch to specific line in target file:

```
vi <file directory> +<n>
```
=======
> shift+G

#### 2. Switch to end of line in normal command line:

> ctrl+E

#### 3. Switch to specific line in target file:

> vi <file directory> +<n>
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59

<!--more-->

#### 4. Look up for filesystems of disk:

<<<<<<< HEAD
```
df -h
```

#### 5. Look up for files in disk:

```
du
```

#### 6. Look up with letter case ignored:

```
grep -i
```

#### 7. Look up for CPU info:

```
htop
```

#### 8. Switch to start of line in normal command line:

```
ctrl+A
```

#### 9. Delete one fragment in normal command line:

```
ctrl+W
```
=======
> df -h

#### 5. Look up for files in disk:

> du

#### 6. Look up with letter case ignored:

> grep -i

#### 7. Look up for CPU info:

> htop

#### 8. Switch to start of line in normal command line:

> ctrl+A

#### 9. Delete one fragment in normal command line:

> ctrl+W
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59

#### 10. Delete one line in vi:

double click D

#### 11. Redo in vi:

double click U

<<<<<<< HEAD
#### 12. for loop for batch processing 

```shell
for i in `docker image ls`; do echo "$i"; done
```

=======
#### 12. for loop for batch processing

``` shell
for i in `docker image ls`; do echo "$i"; done
```
>>>>>>> 38ebd639019f105c786e6269d9bf8a3491ecdd59
