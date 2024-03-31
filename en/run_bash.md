---
lang: en
layout: home
lang-ref: run_bash
---

## Run Bash

In interactive mode with an user Bash executes in cases:

* without arguments or with options excepts `-c`:

```bash
bash
bash -v
bash --verbose
...
```

* in case of `-s` bash can have arguments which are not its options:

```bash
bash -s hello
```

* or when this mode is selected explicity with `-i`.

```bash
bash -i
```

In login mode Bash executes when we login to Bash (in this case the value of $0
will be begin with "-" sign), or when the key `-l` will be set explicity.

##### Turning-on/turning-off readline library

In interactive mode it is used GNU readline library, which can be turned off by
`--noediting`. Without it it won't be accessible such features as command
history by using top arrow key or, for example, command autocompletion with Tab
key. In general, I do not advice to complecite your life.

#### Execute commands from strings

```bash
bash -c 'echo "Execute action from string"'
bash -c 'echo "Execute action from string \
and change value of \$0 to $0"' new_zero
bash -c 'echo "Execute action from string \
with changing \$0 and \$1 and so on"' new_zero new_one
```

Another arguments, followings after the string with a command define ordered variables
$0, $1, $2 ... Where:

$0 -- kepts Bash name, which is used in warnings messages and errors.

#### Execute Bash from Stdout

```bash
echo "ls" | bash -s
```

#### Define ordered variables while starting

First method when they are defined after a string with `-c` key as were shown
above.

The second one is by using `-s`:

```bash
bash -s hello
echo $1
hello
```

Where as you can see the first argument sets a value for $1 but not for $0 as
in case with `-c`.

#### Run bash with a show of runned commands

```bash
bash -v
bash --verbose
```

Now every running command will be shown on a screen before it can be runned. It
is helpful for debugging of a runned script.

#### To know information about current bash

```bash
bash --version
```

#### Short help of bash

```bash
bash --help
```

### Files which is used where bash is starting

In interactive mode or in non-interactive mode with the key `-l`:

* reads commands from /etc/profile if it is accessible:
* then finds files in the next order: ~/.bash_profile, ~/.bash_login, ~/.profile.
  Then run commands from the first of founded of them. To prohibit processing
  commands from those files can be done with `--noprofile` key.

Interactive shell which isn't input one when starting runs commands
from /etc/bash.bashrc and ~/.bashrc. This behaviour can be disabled with
the key `--norc`. When run shell as `sh` that key is set by default.
With the key `--rcfile` you can explicitly define a file from which will be read
commands instead of two previous files.

When run non-interactive shell it is processed a value of BASH_ENV which is used
as a loaded file before commands from a running script will be processed.

m.sh:

```bash
#!/bin/bash

echo $ASDF
```

run m.sh with a loaded file:

```bash
echo "ASDF=1234" > asdf.conf
BASH_ENV=asdf.conf bash ./m.sh
1234
```

An interactive shell with a key `--posix` works by POSIX rules as concerns
processing of loaded files which are got from ENV variable. Other loaded files
in such case doesn't work.

In case of remote shell running commands are processed from file ~/.bashrc.

When run a shell in case of current EUID differs from a real RUID then loaded
file doesn't work and shell functions also. Moreover values for SHELLOPTS, BASHOPTS,
CDPATH, GLOBIGNORE doesn't set. When the key `-p` isn't set EUID canceled to
RUID value.

#### Features when run shell as sh

When run an interactive shell or non-interactive with `-l` it is read and run
from `/etc/profile` and `~/.profile` (it can be prohibited with `--noprofile`).

Instead of BASH_ENV is used ENV value.

rc-files aren't processed, `--norc` by default.

A non-interactive shell when run other loaded files doesn't read.

### Files which is runned when exit from shell

When exit from an (non-)interactive shell whith `exit` command it is runned
commands from file: ~/.bash_logout.
