
# Anoma / Taiga

[Taiga](https://github.com/anoma/taiga), a component of Anoma, is responsible
for generating valid state transition proposals. It establishes the criteria for
valid transactions and offers the tools to create and verify them.

The parts of a transaction are distributed and stored in an encrypted form.

Taiga is based on a [UTXO
model](https://en.wikipedia.org/wiki/Unspent_transaction_output) and was heavily
inspired by [Zcash
Orchard](https://github.com/zcash/zips/blob/main/protocol/protocol.pdf) and
[ZEXE](https://eprint.iacr.org/2018/962).

Let's introduce the concepts of Taiga using an example.

# Two-party exchange

An example of using Taiga to facilitate an exchange between two participants.

See the corresponding [Taiga simulator
code](https://github.com/anoma/taiga-simulator/blob/main/Apps/TwoPartyExchange.juvix).

## Overview

In this scenario there are _Resource_ types **Dolphin**, **A** and **B**. There
are three participants, **Alice**, **Bob** and a **Solver**.

Alice owns:

* 1 **A**
* 2 **B**

Bob owns:

* 1 **Dolphin**

Alice is willing to exchange either 2 **B** or 1 **A** for 1 **Dolphin**. Bob is
willing to exchange 1 **A** for 1 **Dolphin**.

<img alt="two party exchange overview" width="600" src="../.resources/two_party_exchange_overview.png">

## Alice's Partial Transaction

Alice publishes a _partial transaction_ to the network that consumes two resources that she owns:

* 1 **A** resource
* 2 **B** resources

and creates a new resource containing a logic function which encodes her intent, i.e she wants to participate in a transaction that contains a partial transaction in which she receives either 1 **Dolphin** and **2 B** (i.e her **A** resource was spent) or 1 **Dolphin** and 1 **A** (i.e her **1 B** was spent).

<img alt="alice partial transaction" width="600" src="../.resources/alice_partial_tx_1028.png">

## Bob's Partial Transaction

Bob independently publishes a _partial transaction_ to the network that encodes his intent.

It consumes:

* 1 **Dolphin** resource

and creates:

* 1 **A** resource

<img alt="bob partial transaction" width="300" src="../.resources/bob_partial_tx_1028.png">

## Solver's Partial Transaction

The Solver finds both Alice's and Bob's partial transactions it aims to create a
partial transaction which satisfies the logic function and balances the partial
transactions. This means a transaction satisfying both Alice and Bob's wishes
can be published.

It consumes:

* Alice's logic resource

And creates:

* 1 **Dolphin** resource
* 2 **B** resources

<img alt="solver partial transaction" width="600" src="../.resources/solver_partial_tx_1028.png">

This partial transaction consumes a logic function, which means that the partial
transaction must satisfy its logic to be valid.

We can see that the first clause in the logic function is satisfied by the
transaction so it is valid.

## Final Transaction

A transaction is formed from a collection of valid partial transaction that
balance. i.e the quantities of created and consumed resources, for each resource
type in the transaction must balance.

We can check that the quantities of all the resource types balance in this case.

In particular:

* Solver create 2 **B** balances with Alice consume 2 **B**
* Solver create 1 **Dolphin** balances with Bob consume 1 **Dolphin**
* Solver consume **Alice's logic resource** balances with Alice create **Alice's logic resource** 
* Alice consume 1 **A** balances with Bob create 1 **A**

So we conclude that the three partial transaction above together form a transaction.

<img alt="complete transaction" width="1028" src="../.resources/complete_transaction_1028.png">

# Sudoku

An example of participants coordinating a Sudoku game.

See the corresponding [Taiga simulator
code](https://github.com/anoma/taiga-simulator/blob/main/Apps/Sudoku.juvix).

## Overview

For this application there is a _Dealer_ who coordinates the puzzle and a number
of participants who all try to solve the puzzle. The participants are rewarded
for each square of the puzzle they fill in correctly.

There are resource types **Sudoku** which represents a Sudoku grid and **Reward**
which is the token that participants receive for filling in correct squares.

The Sudoku resource has a [logic
function](https://github.com/anoma/taiga-simulator/blob/f9944c2c05a3c7938481bfc1d07b89c8de7ecd10/Apps/Sudoku.juvix#L128)
which checks that the puzzle is valid and that the player claims the correct
reward:

## Start of the game

To start an instance of the application the _Dealer_ publishes a partial
transaction which creates two resources:

* A **Sudoku** resource that contains the initial state of the puzzle.

* A Resource containing a **logic function** that checks the completed
solution to the puzzle.

And consumes another resource:

* A **Reward** resource with quantity equal to the number of unfilled squares in
the puzzle.

<img alt="dealer partial transaction" width="600" src="../.resources/dealer_ptx_1028.png">

## A Player Submits a Partial Solution

A _player_ finds the _dealer_'s partial transaction on the network and publishes a
new _partial transaction_ to fill in some missing squares.

The new partial transaction consumes:

* A **Sudoku** resource which represents the current partial solution to the puzzle.

And creates:

* A **Reward** resource with quantity equal to the number of squares that the
player fills in on the Sudoku grid.

* A **Sudoku** resource that contains an updated Sudoku grid with their
  solutions filled in.
  
<img alt="player 1 partial transaction" width="600" src="../.resources/sudoku_player_1.png">

## A Player Completes the Sudoku

Players can continue to submit partial solutions to the Sudoku, they add to the
chain of partial transactions on the network.

When a player has filled in all the squares on the board their partial
transaction can additionally consume:

* The **dealer's logic function**

<img alt="player 2 partial transaction" width="600" src="../.resources/sudoku_player_2.png">

The chain of partial transactions now balances and so can be published as a
transaction on the network. All the participants obtain their rewards.

<img alt="sudoku complete" width="1028" src="../.resources/sudoku_complete.png">
