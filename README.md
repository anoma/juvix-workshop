> ⚠️  This is a work-in-progress

# Juvix ETHPrague Workshop

## Objectives
- Install and setup Juvix and explore its main features
- Hands-on coding to get familiar with writing Juivx programs
- An introduction to Anoma applications using the Taiga Simulator
- Preview of Juvix compilation to arithmetic circuits using [vamp-ir](https://github.com/anoma/vamp-ir)

## Installing Juvix

### macOS homebrew

``` shell
brew update
brew tap anoma/juvix
brew install juvix
```

### Linux / macOS automatic installer

``` shell
curl --proto '=https' --tlsv1.2 -sSf https://raw.githubusercontent.com/anoma/juvix-installer/main/juvix-installer.sh | sh
```

### Linux manual installation

There is a statically linked binary available at: https://github.com/anoma/juvix/releases/latest/download/juvix-linux-x86_64.tar.gz

## Language Introduction

We will follow the tutorial at https://docs.juvix.org/dev/tutorials/learn/

## Anoma and Taiga Applications

The goal of Juvix is to be used to write applications for [Anoma](https://anoma.net).

Anoma is a system that coordinates transactions between users. 

Applications in Anoma introduce resources that can be traded, and impose
constraints on how transactions involving those resources can behave.

Users submit transactions, which describe a preferred state of the system. Then
the system resolves all user preferences so that the transactions balance
and satisfy the constraints of applications.

Anoma applications that are built using the
[Taiga](https://github.com/anoma/taiga) component use zero-knowledge proofs to
hide sensitive information about transactions.

The implementation of Anoma is not complete. But we can use a
[simulator](https://github.com/anoma/taiga-simulator) to show you how Anoma
applications will work.
