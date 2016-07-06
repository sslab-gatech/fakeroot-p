FakeRoot-P
============
[FakeRoot](https://wiki.debian.org/FakeRoot) is a tool that offers applications the illusion
of root privileges. This is most often used for building packages with correct permissions.
This code is a performance-oriented re-design of FakeRoot, scalable on multi-core architectures.
Please see [pdf](/doc/fakerootp.pdf) for more information.

Building
--------------
Like FakeRoot, FakeRoot-P can be built using either
System V or TCP as a transport mechanism between clients and server.
However, the scalable design of FakeRoot-P is only implemented with the
System V method of communication. When built with the TCP option,
FakeRoot-P retains the lack of scalability of the original FakeRoot code.

SysV IPC is the default; to build for TCP, run configure with
`--with-ipc=tcp` (case-sensitive).


To build, run:
```
cd src/
./configure
make
make install
```

FreeBSD: to compile `--with-ipc=tcp` and `gcc`, make sure the `-pthread` flag
is used.


Notes
--------------
Cases for which the SYSV IPC version fails or causes problems but for
which fakeroot-tcp has been observed to work well include the items
listed below.

  * Multithreaded applications (using pthread)
  * Running under realtime-preempt kernel

Portability: On OS X, only binaries that do NOT rely on Mach-based [e]uid/[e]gid/mode
APIs will correctly use fakeroot altered ownership/permissions.
See README_MACOSX.txt for further information.
