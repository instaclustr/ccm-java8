# ccm-java8

_ccm-java8_ is a simple [CCM](https://github.com/riptano/ccm/) extension that explicitly sets the `JAVA_HOME` environment variable for all CCM-managed
Cassandra nodes to an available Java 1.8 installation, which is required to run Cassandra 3.11 and lower.

**Platforms Currently Supported:** macOS

## Usage

Install it alongside CCM:

`pip install ccm ccm-java8`


## Motivation

While operating systems support the side-by-side installation of multiple Java versions, only one version can be selected as the default
(i.e., what version `java` on `$PATH` points to).

Cassandra's `bin/cassandra` launch script prefers the `java` binary under `$JAVA_HOME`, and will fallback to using the `java` binary on `$PATH` if `$JAVA_HOME` isn't set.
Hence, unless `$JAVA_HOME` or the platform default is explicitly set to a Java 1.8 installation, Cassandra will try, and fail, to start under an incompatible Java version.

_ccm-java8_ works by registering a CCM extension, and hooks into the `append_to_server_env` method that allows extensions to provide additional environment variables
for each Cassandra process started by CCM.
On node start, _ccm-java8_ explicitly sets the `JAVA_HOME` environment variable to a directory containing a Java 1.8 installation, or throws an exception otherwise.