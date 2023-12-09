---
title: /dev/null and 2&>1
date: 2022-10-21 21:27:29
categories: 
- Notes
tags:
- Bash
- en
---

# 1. Notice
1.1 `/dev/null` is the null file. Anything written to it is discarded.
1.2 `2>` means "redirect standard-error" to the given file.
1.3 `2>/dev/null` means "throw away any error messages".
1.4 `1` is stdout. `2` is stderr.
1.5 `2>&1` means redirecting stderr to stdout.

<!--more-->

# 2. Example(s)
``` bash
wget -O /dev/null baidu.com 2>&1 
```

# 3. Reference(s)
Sepehr SaminiSepehr Samini 95544 gold badges1111 silver badges1515 bronze badges, et al. “What Does "/Dev/Null’ Mean at the End of Shell Commands.” Stack Overflow, 1 Feb. 1960, https://stackoverflow.com/questions/13408619/what-does-dev-null-mean-at-the-end-of-shell-commands. 
