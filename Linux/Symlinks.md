When trying to compile the latest gcc version to make a crosscompiler
from x86_64 to i686_elf, I ran into an issue after several steps and I
was stuck with a version of gcc that wasn't backward compatible with
the task at hand. In order to switch from the latest version of gcc (14.0)
to the previous version (12.0) I had to modify the symlink to the gcc lib.

```
which gcc
-> /bin/gcc
ls -ld /bin/gcc
->
```
