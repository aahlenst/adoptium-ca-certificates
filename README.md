# adoptium-ca-certificates

Source code for the Linux packages that provide CA certificates and associated tooling for Eclipse Adoptium runtimes. The packages contain a Java keystore with CA certificates and tooling to automatically synchronize the keystore with the operating system's certificate store.

## Development

### Prerequisites

* Linux or macOS with Docker
* JDK 8 or newer

## Support Policy

### Debian Flavours

* Support policy for Debian: All releases receiving free security updates (incl. LTS, excl. ELTS) plus current development version. See https://wiki.debian.org/DebianReleases.
* Support policy for Ubuntu: All LTS versions (excl. ESM), current regular version plus current development version. See https://wiki.ubuntu.com/Releases.

We do not publish the packages separately for Linux Mint or Raspbian because they are based on either Ubuntu or Debian, and their tools are usually smart enough to infer the correct Debian/Ubuntu repositories to use.

## Common Tasks

### Changing the Supported Debian/Ubuntu Versions

The Debian/Ubuntu versions this package **is built for and uploaded to** is controlled by the variable `deb_versions` in the project's `build.gradle` file. 

The Debian/Ubuntu versions this package **is tested with** is controlled by the class `DebianFlavours` in the source set `packageTest`.

### Changing the Version Number

The version number in the `build.gradle` only affects the version number of the resulting Java artifacts (currently, there are none) and is unrelated to the package versions. The version number of the particular operating system package (deb, rpm) has to be changed in the respective package configuration file:

* **deb**: `dpkg-buildpackage` reads the version number from the top-most entry in `packaging/debian/changelog`. This means that you have to create a new entry at the top of the file to create a new version. See the [Debian Policy Manual](https://www.debian.org/doc/debian-policy/ch-source.html#debian-changelog-debian-changelog) for details.

The *major.minor.patch* versions of Gradle and all operating system packages should match. The operating system package iterations and epochs do not have to match. 
