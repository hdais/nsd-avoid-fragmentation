# avoid-fragmentation implementation for NSD

This is an implementaion of [draft-ietf-dnsop-avoid-fragmentation](https://datatracker.ietf.org/doc/draft-ietf-dnsop-avoid-fragmentation/) (Fragmentation Avoidance in DNS) for NSD.

## Notes
 * Currently it works on Linux only due to getsockopt(IP_MTU) dependency.
 * Avoid-fragmentation mode is enabled on IPv4/UDP sockets only, since NSD already limits maximum size of IPv6/UDP to 1280 bytes.

## How to build
```
git clone https://github.com/hdais/nsd-avoid-fragmentation
cd nsd-avoid-fragmentation
aclocal && autoconf && autoheader
./configure
make
make install
```

## Debugging

Some debug messages available in verbose logging mode:
```
server:
  verbose: 3
```

Debug messages examples:
```
nsd[9837]: notice: avoid-fragmentation mode enabled: forcing maximum IPv4/UDP message size to PMTU
nsd[9847]: info: probe_pmtu: got pmtu to 192.0.2.1 (552 bytes): updating response maxlen from 1232 to 524
```

original README.md follows...

# NSD

[![Travis Build Status](https://travis-ci.org/NLnetLabs/nsd.svg?branch=master)](https://travis-ci.org/NLnetLabs/nsd)
[![Cirrus Build Status](https://api.cirrus-ci.com/github/NLnetLabs/nsd.svg)](https://cirrus-ci.com/github/NLnetLabs/nsd)
[![Packaging status](https://repology.org/badge/tiny-repos/nsd.svg)](https://repology.org/project/nsd/versions)
[![CII Best Practices](https://bestpractices.coreinfrastructure.org/projects/1462/badge)](https://bestpractices.coreinfrastructure.org/projects/1462)

The NLnet Labs Name Server Daemon (NSD) is an authoritative DNS name server.
It has been developed for operations in environments where speed,
reliability, stability and security are of high importance.  If you
have any feedback, we would love to hear from you. Don’t hesitate to
[create an issue on Github](https://github.com/NLnetLabs/nsd/issues/new)
or post a message on the
[NSD mailing list](https://lists.nlnetlabs.nl/mailman/listinfo/nsd-users).
You can learn more about NSD by reading our
[documentation](https://nsd.docs.nlnetlabs.nl/).

## Compiling

Make sure you have the following installed:
  * C toolchain (the set of tools to compile C such as a compiler, linker, and assembler)
  * OpenSSL, with its include files (usually these are included in the "dev" version of the library)
  * libevent, with its include files (usually these are included in the "dev" version of the library)
  * flex
  * bison

The repository does not contain `./configure`, but you can generate it like
this (note that the `./configure` is included in release tarballs so they do not have to be generated):

```
aclocal && autoconf && autoheader
```

NSD can be compiled and installed using:

```
./configure && make && make install
```

## NSD configuration

The configuration options for NSD are described in the man pages, which are
installed (use `man nsd.conf`) and are available on the NSD
[documentation page](https://nsd.docs.nlnetlabs.nl/).

An example configuration file is located in
[nsd.conf.sample](https://github.com/NLnetLabs/nsd/blob/master/nsd.conf.sample.in).
