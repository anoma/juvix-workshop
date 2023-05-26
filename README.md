> ⚠️  This is a work-in-progress

# Juvix ETHPrague Workshop

## Objectives
- Install and setup Juvix and explore its main features
- Hands-on coding to get familiar with writing Juivx programs
- An introduction to Anoma applications using the Taiga Simulator
- Preview of Juvix compilation to arithmetic circuits using [vamp-ir](https://github.com/anoma/vamp-ir)

## Table of Contents
- [Installing Juvix](#installing-juvix)
- [IDE Support](#ide-support)
    - [VSCode](#vscode)
    - [Emacs](#emacs)
- [Language Introduction](#language-introduction)
- [Applications](#applications)
    - [Hello World!](#hello-world) ([Source Code](./hello-world/))
    - [Arithmetic Circuits](#arithmetic-circuits) ([Source Code](./arithmetic-circuits/))
    - [Anoma/Taiga Sudoku](#anoma-taiga-sudoku) ([Source Code](./taiga-sudoku/))

## Installing Juvix

Use one of the following options to install Juvix on your machine. We support
Linux on x86_64 architecture and macOS on both x86_64 and aarch64 (M1)
architectures.

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

It will install the Juvix compiler, the required LLVM toolchain, and setup your shell environment.

### Manual installation

There are also binaries for the Juvix compiler available to download:

| OS / Architecture                                                                                           |
|-------------------------------------------------------------------------------------------------------------|
| [Linux x86_64](https://github.com/anoma/juvix/releases/latest/download/juvix-linux-x86_64.tar.gz)           |
| [macOS x86_64](https://github.com/anoma/juvix/releases/latest/download/juvix-macos-x86_64.tar.gz)           |
| [macOS aarch64 (M1/M2)](https://github.com/anoma/juvix/releases/latest/download/juvix-macos-aarch64.tar.gz) |

The Juvix compiler requires an LLVM toolchain to be present in your PATH.

## Language Introduction

We will follow the tutorial at https://docs.juvix.org/dev/tutorials/learn/

## Applications

### Hello World

Compile and run the famous Hello World program:

``` shell
juvix compile hello-world/HelloWorld.juvix && ./HelloWorld
```

### Arithmetic Circuits

### Anoma / Taiga Sudoku

A simulation of an [Anoma](https://anoma.net) application built using the
[Taiga](https://github.com/anoma/taiga) execution model.

