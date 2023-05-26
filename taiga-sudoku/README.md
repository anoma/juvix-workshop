# Anoma / Taiga Sudoku

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
