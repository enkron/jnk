## Bash
### Strict mode
```bash
#!/bin/bash

set -eu -o pipefail -o posix

function main() {
    echo hello
}

main "${@}"
```

### Colorize `less`
below instructions related to Arch based Linux distros, but definetely
can be easily applied to another distribution with minimum changes.

First, of all install a package called `source-highlight` - it converts
source code to syntax highlighted document.

It could be search with next command:
```bash
sudo pacman -Ss source-highlight
```
and consequently installed:
```bash
sudo pacman -S source-highlight
```
Next, check that the package installed correctly and find a path to the
`src-hilite-lesspipe.sh` script (here's what's needed for `less`
highlighting)
```bash
pacman -Qi source-highlight # check info about the package

# find a highlighting script location, in my case output of the below
# command -> source-highlight /usr/bin/src-hilite-lesspipe.sh
pacman -Ql |grep source-highlight |grep less
```
And finally add below environment variables into `bashrc` file
```bash
export LESSOPEN="| /usr/bin/src-hilite-lesspipe.sh %s"
export LESS=" -R "
```

### List bash's options for the current shell
It's sometimes useful to check bash's options which are setup for the
current shell. For instance, we can turn off bash history recording with
the following command:

```bash
set +o history # set +H works either
# Using + rather than - causes these options to be turned  off.
```

After that we can check shell options with the below command:

```bash
printf %s\\n "$-"
```
