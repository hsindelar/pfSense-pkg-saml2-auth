# Building for FreeBSD 16 / pfSense 25.11

This package now supports FreeBSD 16 (pfSense 25.11). Here's how to build it:

## Local Build with Vagrant

To build a package for FreeBSD 16 locally using Vagrant:

```bash
# Set the FreeBSD version to 16
export FREEBSD_VERSION="freebsd/FreeBSD-16.0-CURRENT"
export BUILD_VERSION="0.0_0-dev"

# Run the build script
sh vagrant-build.sh
```

The resulting package will be: `pfSense-pkg-saml2-auth-0.0_0-dev.pkg`

## Building for Multiple Versions

To build for all supported versions, run the build script multiple times with different FreeBSD versions:

```bash
# FreeBSD 14 (pfSense 2.7.x)
FREEBSD_VERSION="freebsd/FreeBSD-14.0-CURRENT" BUILD_VERSION="0.0_0-dev-freebsd14" sh vagrant-build.sh

# FreeBSD 15 (pfSense 2.8.x)
FREEBSD_VERSION="freebsd/FreeBSD-15.0-CURRENT" BUILD_VERSION="0.0_0-dev-freebsd15" sh vagrant-build.sh

# FreeBSD 16 (pfSense 25.11)
FREEBSD_VERSION="freebsd/FreeBSD-16.0-CURRENT" BUILD_VERSION="0.0_0-dev-freebsd16" sh vagrant-build.sh
```

## Installing on pfSense 25.11

Once you've built the package, copy it to your pfSense 25.11 system and install:

```bash
# Copy the package to pfSense
scp pfSense-pkg-saml2-auth-0.0_0-dev.pkg admin@your-pfsense-ip:/tmp/

# SSH into pfSense and install
ssh admin@your-pfsense-ip
pkg add /tmp/pfSense-pkg-saml2-auth-0.0_0-dev.pkg
```

## Vagrant Box Availability

Note: Make sure the FreeBSD 16 Vagrant box is available. If `freebsd/FreeBSD-16.0-CURRENT` doesn't exist yet, you may need to:

1. Check [Vagrant Cloud](https://app.vagrantup.com/freebsd) for available FreeBSD 16 boxes
2. Use an alternative box name if available
3. Wait for official FreeBSD 16 Vagrant boxes to be published

You can check available boxes with:
```bash
vagrant box list
```

Or search online:
```bash
curl https://app.vagrantup.com/api/v1/search?q=freebsd%2016
```
