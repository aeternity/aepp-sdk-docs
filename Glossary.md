---
layout: page
title: Glossary
navigation: 50
---

# æternity glossary

## Overview

This document is an overview of both æternity-specific and blockchain concepts and terms. It's intended to help bring newcomers up to speed with both the æternity project, and blockchain concepts in general.

## æternity
æternity is a decentralized, public blockchain that uses the GHOST consensus
protocol, with Proof-of-Work (PoW) for security and Proof-of-Stake (PoS) for
governance. æternity is an account-based system, like Ethereum, and does not use
Bitcoin-style unspent transaction outputs (UTXO). 

Real-world data can interface with smart contracts through decentralized
"oracles". Scalability and trustless Turing-complete state channels set æternity
apart from other Blockchain 2.0 projects.

[Source](https://github.com/aeternity/aeternity-reimagined/blob/master/overview.md)

## æternity token
The æternity token (AE) is used as payment for any resources that users consume
on the platform, e.g. sending payments, using oracles, etc. The distribution of
AE in the genesis block will be determined by a smart contract hosted on
Ethereum. More AE will be created via mining.

## Application-specific integrated circuit (ASIC)
An application-specific integrated circuit (ASIC) /ˈeɪsɪk/, is an integrated
circuit (IC) customized for a particular use, rather than intended for
general-purpose use. For example, a chip designed to run in a digital voice
recorder or a high-efficiency Bitcoin miner is an ASIC. Application-specific
standard products (ASSPs) are intermediate between ASICs and industry standard
integrated circuits like the 7400 series or the 4000 series.

[Source](https://en.wikipedia.org/wiki/Application-specific_integrated_circuit)

## Blockchain
A block chain is a transaction database shared by all nodes participating in a
system based on the Bitcoin protocol. A full copy of a currency's block chain
contains every transaction ever executed in the currency. With this information,
one can find out how much value belonged to each address at any point in
history.

This ledger of past transactions is called the block chain as it is a chain of
blocks. The block chain serves to confirm transactions to the rest of the
network as having taken place.

[Source](https://en.bitcoin.it/wiki/Block_chain)
[Source](https://www.bitcoinmining.com/)

## Cuckoo Cycle
æternity uses Cuckoo Cycle as the ASIC-resistant mining algorithm to avoid
centralizing mining power in the hands of a few large mining pools.

Cuckoo Cycle is the first graph-theoretic proof-of-work, and the most memory
bound, yet with instant verification.

From this point of view, Cuckoo Cycle is a very simple PoW, requiring hardly any
code, time, or memory to verify.

Finding a 42-cycle, on the other hand, is far from trivial, requiring
considerable resources, and some luck (for a given header, the odds of its graph
having a L-cycle are about 1 in L).

Its large memory requirements make single-chip ASICs economically infeasable for
Cuckoo Cycle.

## GHOST consensus protocol
GHOST is short for the Greedy Heaviest Observed Subtree chain selection rule
which was a proposed modification for the Bitcoin blockchain.

GHOST orignally was a protocol modification, a chain selection rule, that makes
use of blocks that are off the main chain to obtain a more secure and scalable
system.

With that modification, it is possible to speed up the blockchain to a velocity
of up to 1 block per second. The result is a general higher possible transaction
rate without compromising the blockchain consensus and security.

[Source](https://ethereum.stackexchange.com/questions/314/what-is-ghost-and-what-is-its-relationship-to-frontier-and-casper

## Consensus
When several nodes (usually most nodes on the network) all have the same blocks
in their locally-validated best block chain.

[Source](https://bitcoin.org/en/glossary/consensus)

## Faucet (cryptocurrency)
Bitcoin faucets are a reward system, in the form of a website or app, that
dispenses rewards in the form of a satoshi, which is a hundredth of a millionth
BTC, for visitors to claim in exchange for completing a captcha or task as
described by the website. There are also faucets that dispense alternative
cryptocurrencies.

## Genesis block
A genesis block is the first block of a block chain. Modern versions of Bitcoin
number it as block 0, though very early versions counted it as block 1. The
genesis block is almost always hardcoded into the software of the applications
that utilize its block chain. It is a special case in that it does not reference
a previous block, and for Bitcoin and almost all of its derivatives, it produces
an unspendable subsidy.

[Source](https://en.bitcoin.it/wiki/Genesis_block)

## Hashcash PoW
Hashcash is a proof-of-work algorithm that requires a selectable amount of work
to compute, but the proof can be verified efficiently. For email uses, a textual
encoding of a hashcash stamp is added to the header of an email to prove the
sender has expended a modest amount of CPU time calculating the stamp prior to
sending the email. In other words, as the sender has taken a certain amount of
time to generate the stamp and send the email, it is unlikely that they are a
spammer. The receiver can, at negligible computational cost, verify that the
stamp is valid. However, the only known way to find a header with the necessary
properties is brute force, trying random values until the answer is found;
though testing an individual string is easy, if satisfactory answers are rare
enough it will require a substantial number of tries to find the answer.

## Merkle tree (hash tree)
In cryptography and computer science, a hash tree or Merkle tree is a tree in
which every leaf node is labelled with the hash of a data block and every
non-leaf node is labelled with the cryptographic hash of the labels of its child
nodes. Hash trees allow efficient and secure verification of the contents of
large data structures. Hash trees are a generalization of hash lists and hash
chains.

Hash trees can be used to verify any kind of data stored, handled and
transferred in and between computers. They can help ensure that data blocks
received from other peers in a peer-to-peer network are received undamaged and
unaltered, and even to check that the other peers do not lie and send fake
blocks.

## Mining
In cryptocurrency networks, mining is a validation of transactions. For this
effort, successful miners obtain new cryptocurrency as a reward. The reward
decreases transaction fees by creating a complementary incentive to contribute
to the processing power of the network. The rate of generating hashes, which
validate any transaction, has been increased by the use of specialized machines
such as FPGAs and ASICs running complex hashing algorithms like SHA-256 and
Scrypt. This arms race for cheaper-yet-efficient machines has been on since
the day the first cryptocurrency, bitcoin, was introduced in 2009. However,
with more people venturing into the world of virtual currency, generating hashes
for this validation has become far more complex over the years, with miners
having to invest large sums of money on employing multiple high performance
ASICs. Thus the value of the currency obtained for finding a hash often does not
justify the amount of money spent on setting up the machines, the cooling
facilities to overcome the enormous amount of heat they produce, and the
electricity required to run them.

Bitcoin mining is intentionally designed to be resource-intensive and difficult
so that the number of blocks found each day by miners remains steady. Individual
blocks must contain a proof of work to be considered valid. This proof of work
is verified by other Bitcoin nodes each time they receive a block. Bitcoin uses
the hashcash proof-of-work function.

[Source](https://en.wikipedia.org/wiki/Cryptocurrency#Mining)
[Source](https://www.bitcoinmining.com/)

## Nonce (cryptography)
In cryptography, a nonce is an arbitrary number that can only be used once. It
is similar in spirit to a nonce word, hence the name. It is often a random or
pseudo-random number issued in an authentication protocol to ensure that old
communications cannot be reused in replay attacks. They can also be useful as
initialization vectors and in cryptographic hash functions.

Nonces are used in proof-of-work systems to vary the input to a cryptographic
hash function so as to obtain a hash for a certain input that fulfills certain
arbitrary conditions. In doing so, it becomes far more difficult to create a
"desirable" hash than to verify it, shifting the burden of work onto one side of
a transaction or system. For example, proof of work, using hash functions, was
considered as a means to combat email spam by forcing email senders to find a
hash value for the email (which included a timestamp to prevent pre-computation
of useful hashes for later use) that had an arbitrary number of leading zeroes,
by hashing the same input with a large number of nonce values until a
"desirable" hash was obtained.

[Source](https://en.wikipedia.org/wiki/Cryptographic_nonce)

## Oracle
Oracles are trusted entities signing claims about the state of the world - RPCs,
gateways to input/output with the physical realm.

They form the ability to refer to values from real-world data. 

An oracle is a mechanism that tells the blockchain facts about the real-world we
live in (e.g. the weather, the closing price of Apple shares on a particular
date, sports events, or human deaths). æternity's oracle system(21) uses the
same governance mechanism as the æternity blockchain itself, it does not require
a separate governance layer on top of the æternity main-net (22) (as with Augur
on top of Ethereum).

Typed oracles as primitives on the blockchain provide a well-defined way for
smart contracts to interface with data from the outside world. Data-feeds from
individuals or institutions can directly interface with the blockchain and
provide data for smart contracts.

[Source](https://www.ledger.fr/2016/08/31/hardware-pythias-bridging-the-real-world-to-the-blockchain)
[Source](https://en.wikipedia.org/wiki/%C3%86ternity#Decentralized_Oracle)

## Proof-of-stake (PoS)
Proof of stake (PoS) is a type of algorithm by which a cryptocurrency blockchain
network aims to achieve distributed consensus. In PoS-based cryptocurrencies,
the creator of the next block is chosen via various combinations of random
selection and wealth or age (i.e., the stake). In contrast, the algorithm of
proof-of-work-based cryptocurrencies such as bitcoin uses mining; that is, the
solving of computationally intensive puzzles to validate transactions and create
new blocks.

Proof-of-stake currencies can be more energy efficient than currencies based on
proof-of-work algorithms.

[Source](https://en.wikipedia.org/wiki/Proof-of-stake)

## Proof-of-work system (PoW)
A proof-of-work (PoW) system (or protocol, or function) is an economic measure
to deter denial of service attacks and other service abuses such as spam on a
network by requiring some work from the service requester, usually meaning
processing time by a computer.

A key feature of these schemes is their asymmetry: the work must be moderately
hard (but feasible) on the requester side but easy to check for the service
provider. This idea is also known as a CPU cost function, client puzzle,
computational puzzle or CPU pricing function. It is distinct from a CAPTCHA,
which is intended for a human to solve quickly, rather than a computer.

[Source](https://en.wikipedia.org/wiki/Proof-of-work_system)

## ReasonML
Reason lets you write simple, fast and quality type safe code while leveraging
both the JavaScript & OCaml ecosystems.

[Source](https://reasonml.github.io/)

## Smart Contract
A smart contract is a computer protocol intended to digitally facilitate,
verify, or enforce the negotiation or performance of a contract. Smart contracts
allow the performance of credible transactions without third parties. These
transactions are trackable and irreversible. 

The aim of smart contracts is to provide security that is superior to
traditional contract law and to reduce other transaction costs associated with
contracting. Various cryptocurrencies have implemented types of smart contracts.

With the present implementations, based on blockchains, "smart contract" is
mostly used more specifically in the sense of general purpose computation that
takes place on a blockchain or distributed ledger. In this interpretation, used
for example by the Ethereum Foundation or IBM, a smart contract is not
necessarily related to the classical concept of a contract, but can be any kind
of computer program.

A major limitation of smart contracts is that they are unable to communicate
with resources external to the blockchain they are secured on. In practice, this
means that smart contracts are not able to trigger based on real-life
events. This is known as "the oracle problem", after test oracles. Oracles
provide external data and trigger smart contract executions when pre-defined
conditions are met, providing connectivity to the outside world.

The overreaching functional goal of Æternity smart contracts is to be able to
execute code on the chain. That is, code execution that is verified by a miner
and which can alter the state of the chain. A contract runs on a virtual
machine. A smart contract is associated with a virtual machine for the execution
of that contract. The AEternity blockchain supports four virtual machines.

Further reading (here)(https://en.wikipedia.org/wiki/Smart_contract  ) and (here)(https://github.com/aeternity/protocol/blob/master/contracts/contracts.md)

## Solution-verification PoW
Solution-verification protocols do not assume such a link: as a result the
problem must be self-imposed before a solution is sought by the requester, and
the provider must check both the problem choice and the found solution. Most
such schemes are unbounded probabilistic iterative procedures such as Hashcash.

## State channel
State channels enable highly scalable, trustless transactions of value and
purely functional, easily verifiable Turing-complete smart contracts.

State channels offer a way to scale “off-chain” by only storing channel opening
and closing information on the blockchain. Two parties deposit tokens into a
channel when they open it and the sum of two deposits is the only amount of
tokens that can be used within that channel. The state of the channel is the
current balance of each party, co-signed by both parties. There can be multiple
exchanges of state between the parties but only the last undisputed state
becomes the final closing state of the channel. Each message in the channel
carries an ever-increasing counter and the message with the highest counter
value is considered to be the last state.

State channels come from the realization that, for most purposes, only the
actors involved in a smart contract are required to know about it. Two or more
actors lock a state and a contract on the blockchain and then perform signed
transactions between themselves, off of the public network (or off-chain). The
final state is then written to the blockchain. If the end result is disputed,
the series of signed off-chain transactions can be uploaded to the blockchain
for verification or dispute resolution

[Source](https://github.com/aeternity/aeternity-reimagined/blob/master/state-channels.md  
[Source](https://en.wikipedia.org/wiki/%C3%86ternity#State_channels

## Solidity
Solidity is a contract-oriented, high-level language for implementing smart
contracts. It was influenced by C++, Python and JavaScript and is designed to
target the Ethereum Virtual Machine (EVM).

[Source](https://solidity.readthedocs.io/en/v0.4.20/)

## Sophia (programming language)
An AEternity BlockChain Language - Sophia is a dialect of ReasonML.

Sophia is customized for smart contracts, which can be published to a blockchain
(the AEternity BlockChain). Thus some unnecessary features of Reason (and
OCaml - since Reason is closely related to OCaml) have been removed, and some
blockchain specific primitives, constructions and types have been added.

The Functional Typed Warded Virtual Machine is used to efficiently and safely
execute contracts written in the Sophia language.

[Source](https://github.com/aeternity/protocol/blob/master/contracts/sophia.md)
[Source](https://github.com/aeternity/protocol/blob/master/contracts/aevm.md)

## Virtual Machine
A virtual machine is a computer program which provides the services usually provided by a computer, but which runs on another computer, which may be of the same type, but as easily may not. Blockchains provide virtual machines in order to enable programs to be run on the blockchain. 

The Ethereum Virtual Machine focuses on providing security and executing
untrusted code by computers all over the world. To be more specific, this
project focuses on preventing Denial-of-service attacks, which have become
somewhat common in the cryptocurrency world. Moreover, the EVM ensures programs
do not have access to each other’s state, ensuring communication can be
established without any potential interference.

To put this into a language everyone can understand, the Ethereum Virtual
Machine is designed to serve as a runtime environment for smart contracts based
on Ethereum. As most cryptocurrency enthusiasts are well aware of, smart
contracts are very popular these days. This technology can be used to
automatically conduct transactions or perform specific actions on the Ethereum
blockchain. Many people predict smart contracts will help revolutionize finance
and other industries over the coming years.

The AEternity blockchain supports four virtual machines.

- HLM - A high level machine for executing logical formulas and blockchain operations.
- FTWVM - A Functional Typed Warded Virtual Machine
- AEVM - A version of the Ethereum VM
- FAEVM - A fast version of the Ethereum VM

[Source](https://themerkle.com/what-is-the-ethereum-virtual-machine/)
[Source](https://github.com/aeternity/protocol/blob/master/contracts/aevm.md)

