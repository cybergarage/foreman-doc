![foreman_logo](./img/icon.png)

# Developers Guide

This document aims to describe an introduction to Foreman committers and contributors.

## Coding Styles

TBD

## Commit Guidelines

TBD

## Building and Testing

Foreman consists of two main packages, [foreman-cc](https://github.com/cybergarage/foreman-cc) and [foreman-go](https://github.com/cybergarage/foreman-go).

### foreman-cc

To build [foreman-cc](https://github.com/cybergarage/foreman-cc), you have to install latest [XCode](https://developer.apple.com/xcode/) from AppStore and the following commands using [Homebrew](https://brew.sh).

```
brew install automake autoconf folly
```

#### MacOSX

##### Buiding from Source
```
git clone https://github.com/cybergarage/foreman-cc.git
cd foreman-cc/
./boostrap
./configure_macosx
make
make install
```

##### Homebrew

TBD

### foreman-go

#### MacOSX

##### Setup

```
git clone https://github.com/cybergarage/foreman-go.git
source setup
make test
```