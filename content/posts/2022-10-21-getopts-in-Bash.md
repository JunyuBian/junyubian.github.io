---
title: getopts in Bash
date: 2022-10-21 14:17:29
categories: 
- Notes
tags:
- Bash
- en
---

# 1. Notice
1.1 `getopts` is different from `getopt`.
1.2 `getopts` runs on any system running bash in POSIX mode (e.g., set -o posix), `getopt` is a system tool varies in different systems.
1.3 `getopts` parses short options, which are a single dash ("-") and a letter or digit.e.g. -2, -d, and -D. It can also parse short options in combination, for instance -2dD. But each option will be treated seperately, i.e. -2dD = -2 -d -D not equal -"2dD", will need `getopt` to cope with -"2dD".

<!--more-->

# 2. Syntax
``` bash
getopts optstring optname [ arg ]
```
2.1 Every time you run `getopts`, it looks for one of the options defined in `optstring`. If it finds one, it places the option letter in a variable named `optname`. If the option does not match those defined in `optstring`, `getopts` sets variable `optname` to a question mark ("?"), will need `\?` in `switch ... case`.

2.2 If the option is expecting an argument, `getopts` gets that argument, and places it in `$OPTARG`. If an expected argument is not found, the variable optname is set to a colon ( ":" ). `Getopts` then increments the positional index, `$OPTIND`, that indicates the next option to be processed, don't need `\:` in `switch ... case`.

2.3 However, if you put a colon at the beginning of the `optstring`, `getopts` runs in "silent error checking mode." It will not report any verbose errors about options or arguments, and you need to perform error checking in your script.

2.4 In silent mode, if an option is unexpected, getopts sets `optname` to "?" and `$OPTARG` to the unknown option character.

2.5 If the option is OK but an expected argument is not found, `optname` is set to a colon ( ":" ) and `$OPTARG` is set to the unknown option character.

2.6 `\?` needs to appear before `:` in `switch ... case` for error checking, e.g.

```bash
while getopts ":hi:" option; do
  case "$option" in
    h) 
      echo "help function"
      ;;
    i) 
      ilist=$OPTARG
      ;;
    \?) 
      echo $option
      echo "Invalid option"
      ;;
    :) 
      echo $option
      echo "no argument"
      ;;  
  esac
done
```

2.7 The special option of two dashes ("--") is interpreted by getopts as the end of options.

# 3. Reference(s)
“Bash Getopts Builtin Command Help and Examples.” Help and Examples, 1 Feb. 2021, https://www.computerhope.com/unix/bash/getopts.htm. 
