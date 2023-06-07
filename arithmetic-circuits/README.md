## Arithmetic Circuits / Zero-knowledge Proofs

This directory contains [source code](./MidSquareHash.juvix) implementing the mid-square hash function.

Use following steps to compile the Juvix file to a vampir input and then use
[vamp-ir](https://github.com/anoma/vamp-ir) to compile to a circuit, generate
and verify a proof.

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
