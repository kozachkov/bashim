---
lang: en
layout: home
lang-ref: comparison_bash
---

### Comparison Bash to Perl

### Output

Bash:

```bash
echo "Output with newline"
echo -n "Output without newline"
```

In perl

With `print`

```perl
print "Output with newline\n";
print "Output without newline";
```

With `print` previously change a value of the special variable $\

```perl
$\="\n";
print "Output with newline on the end";
```

With `say` which  it's necessary to enable in perl by `use feature "say";`
or by `use v5.10;` line which also "contains" `use feature "say"` line.
It also prints a line with newline on the end.

```perl
say "Output with newline on the end";
```

#### Functions

In Bash:

```bash
#!/bin/bash

usage() {
  echo "I don't advise"
}

function help {
  echo "I won't help"
}

function no() {
  echo "No"
}

# Functions must be defined before their calls

usage
help;
no
```

Perl:

```perl
use strict;
use warnings;

# It's allowed to call functions (subroutines) which are defined after call.

usage();

sub usage {
    print "And I can\n";
}
```

#### Change the current directory

Bash:

```bash
cd /foo
```

Perl:

```bash
chdir("/foo");
```
