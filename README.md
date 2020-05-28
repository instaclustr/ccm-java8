# ccm-java8

[![PyPi Badge](https://img.shields.io/pypi/v/ccm-java8)](https://pypi.org/project/ccm-java8/)

_ccm-java8_ is a [Cassandra Cluster Manager](https://github.com/riptano/ccm) (CCM) extension that explicitly sets the `JAVA_HOME` environment variable for all CCM-managed
Cassandra nodes (and related tools) to an available Java 8 installation, which is required to run Cassandra 3.11 and lower.

Platforms Currently Supported:
* macOS
* Linux
    * Arch
    * Debian-based
    * RHEL-based

## Usage

_ccm-java8_ is available on [PyPI](https://pypi.org/project/ccm-java8/).

1. Install it alongside CCM:

       pip install ccm ccm-java8

1. Run CCM commands as normal.

    Cassandra and various tools will launch using the Java 8 VM.
    
    If no Java 8 VM can be found, CCM will refuse to start.
    Install Java 8 if this occurs.


## Motivation

Many operating systems support the side-by-side installation of multiple Java versions, yet only one version can be selected as the default
(i.e., what version of `java` is on `$PATH`).

Cassandra's `bin/cassandra` launch script prefers the `java` binary under `$JAVA_HOME`, and will fallback to using the `java` binary on `$PATH` if `$JAVA_HOME` isn't set.
Hence, unless `$JAVA_HOME` or the platform default is explicitly set to a Java 8 installation, Cassandra will try, and fail, to start under an incompatible Java version.

_ccm-java8_ works by registering a CCM extension that when loaded by CCM explicitly sets the `JAVA_HOME` environment variable to a directory containing a Java 8 installation, or throws an exception otherwise.

Older versions used to register a hook into the `append_to_server_env` function, but this function doesn't get called for tools (`nodetool`, `sstabledump`, etc.).
The current version sets the `JAVA_HOME` environment variable globally in the CCM Python process, which gets inherited by all sub-processes launched by CCM.