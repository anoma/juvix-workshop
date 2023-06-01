<h1> Juvix ETHPrague Workshop</h1>
<h1><a href="https://bit.ly/juvix-eth">https://bit.ly/juvix-eth</a></h1>
<img alt="tara mascot smiling" width="400" src="./.resources/tara-smiling.png">
<p>
  <a href="https://discord.gg/PfaaFVErHt"><img src="https://img.shields.io/discord/952881043520774194?logo=discord"/></a>
</p>

## Table of Contents
- [Introduction](#introduction)
- [Installing Juvix](#installing-juvix)
- [IDE Setup](#ide-setup)
    - [VSCode](#vscode)
    - [Emacs](#emacs)
- [Juvix Documentation](#juvix-documentation)
- [Workshop Exercises](#workshop-exercises)
- [Juvix Programs](#juvix-programs)
    - [Hello World!](#hello-world) ([Source Code](./hello-world/))
    - [Anoma Applications](#anoma-applications) ([Source Code](https://github.com/anoma/taiga-simulator))
    - [Arithmetic Circuits](#arithmetic-circuits--zero-knowledge-proofs) ([Source Code](./arithmetic-circuits/))

## Introduction

Welcome to Juvix!

In this workshop we will install the Juvix compiler and related tools, take a
tour of the Juvix language, and explore some Juvix applications.

## Installing Juvix

Please use one of the following options to install the Juvix compiler. Juvix is
supported on Linux x86_64 and macOS x86_64 or aarch64 (M1/M2).

### Prerequisites

The Juvix compiler requires [the LLVM/clang compiler](https://llvm.org) to be available on your system PATH in order to build native binaries.

### macOS homebrew

If you use the [Homebrew package manager](https://brew.sh) you can use our tap:

``` shell
brew update
brew tap anoma/juvix
brew install juvix
```

### Linux / macOS automatic installer

To install for linux or macOS run the following in a terminal (as a non-root user):

``` shell
curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/anoma/juvix-installer/main/juvix-installer.sh | sh
```

### Manual installation

There are also binaries for the Juvix compiler available to download

| OS / Architecture                                                                                           |
|-------------------------------------------------------------------------------------------------------------|
| [Linux x86_64](https://github.com/anoma/juvix/releases/latest/download/juvix-linux-x86_64.tar.gz)           |
| [macOS x86_64](https://github.com/anoma/juvix/releases/latest/download/juvix-macos-x86_64.tar.gz)           |
| [macOS aarch64 (M1/M2)](https://github.com/anoma/juvix/releases/latest/download/juvix-macos-aarch64.tar.gz) |

## IDE Setup

### Visual Studio Code

First install visual studio code from the Microsoft website https://code.visualstudio.com/download

In the extension tab search for `juvix` and install the extension that features the Tara logo.

See the [vscode-juvix repository](https://github.com/anoma/vscode-juvix) for usage information.

### Emacs

To get started, clone the [juvix-mode repository](https://github.com/anoma/juvix-mode.git)

``` shell
git clone https://github.com/anoma/juvix-mode.git
```

And add the following lines to your Emacs configuration file:

``` emacs-lisp
(push "/path/to/juvix-mode/" load-path)
(require 'juvix-mode)
```

See the [juvix-mode repository](https://github.com/anoma/juvix-mode.git) for usage information.

## Juvix Documentation

The full documentation for Juvix is available at https://docs.juvix.org

## Workshop Exercises

Try the workshop exercises in the Juvix project at [exercises/Exercises.juvix](./exercises/Exercises.juvix)

## Juvix Programs

### Hello World

Compile and run the famous Hello World program:

``` shell
juvix compile hello-world/HelloWorld.juvix && ./HelloWorld
```

### Anoma Applications

One of the goals of Juvix is to be used as language to write applications for
the [Anoma protocol](https://anoma.net).

We will explore [simulations](https://github.com/anoma/taiga-simulator) of an
[Anoma](https://anoma.net) application built using the
[Taiga](https://github.com/anoma/taiga) execution model.

### Arithmetic Circuits / Zero-knowledge Proofs

The Juvix compiler has a backend that targets the
[vamp-ir](https://github.com/anoma/vamp-ir) arithmetic circuit intermediate
language. `vamp-ir` can then be used to generate zero-knowledge proofs that
relate inputs and output of the program.

Not all Juvix programs can be compiled to vamp-ir. Future releases of Juvix will
improve vamp-ir support.

For example, this is how to compile the [Juvix
implementation](./arithmetic-circuits/MidSquareHash.juvix) of the mid-square
hash algorithm:

``` shell
cd arithmetic-circuits
juvix compile -t vampir MidSquareHash.juvix
```

The vamp-ir file can then be compiled to a PLONK circuit:

``` shell
vamp-ir plonk setup -m 10 -o params.pp
vamp-ir plonk compile -u params.pp -s MidSquareHash.pir -o circuit.plonk
```

A zero-knowledge proof that `hash 1367` is equal to `3` can then be generated from the circuit:

``` shell
vamp-ir plonk prove -u params.pp -c circuit.plonk -o proof.plonk -i MidSquareHash.json
```

This proof can then be verified:

``` shell
vamp-ir plonk verify -u params.pp -c circuit.plonk -p proof.plonk
```
