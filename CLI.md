The æternity command line interface

## Summary
æternity's SDKs each feature a command-line interface which you can use to invoke the blockchain's features. The CLIs all have the same name and syntax, which are described here. However not all have a full feature set. An entry in [square brackets] indicates which SDKs support a feature, using the codes
- G go
- J javascript
- P python

So [GP] indicates that a feature is only available in Go and Python.

## Overview

The command-line interface is invoked using the command `aecli`. Depending on where it's installed on your system you may have to give a path when you invoke it. 

## General usage
If you invoke `aecli` with no arguments it shows basic usage:
```
$ ./aecli 
The command line client for the Aeternity blockchain

Usage:
  aecli [command]

Available Commands:
  chain       Query the state of the chain
  config      Print the configuration of the client
  help        Help about any command
  inspect     Inspect an object of the blockchain
  name        A brief description of your command
  wallet      Interact with a wallet

Flags:
  -c, --config string   config file to load (defaults to $HOME/.aeternity/config.yaml
      --debug           enable debug
  -h, --help            help for aecli
      --json            print output in json format
      --version         version for aecli

Use "aecli [command] --help" for more information about a command.
```

The general groupings of commands are:
- `chain`  commands do not require a public or private key and give information about the state of the chain. None of the chain commands change the state of the chain at all.
- `config` displays the client's configuration file and can write the configuration to disk.
- `help` does what one would expect and is described here no further.
- `inspect` allows you to look at the objects on the blockchain
- `name` allows interaction with the naming system
- `wallet` commands cover a set of functions which operate with a keypair, from transferring tokens to registering names to invoking smart contracts.

## The chain group

```
$ ./aecli chain
Query the state of the chain

Usage:
  aecli chain [command]

Available Commands:
  play        Query the blocks of the chain one after the other
  top         Query the top block of the chain
  version     Get the status and version of the node running the chain
```
These commands display basic information about the blockchain and require little explanation. Play moves backwards through the blockchain displaying blocks and transactions

## The inspect group
The inspect command allows you to see inside various æternity types. Because each æternity type starts with two letters identifying what sort of thing it is, you can throw anything you like at inspect, and it will bravely try to do the right thing.

#### inspect public key
```
$ ./aecli inspect ak_XeSuxD8wZ1eDWYu71pWVMJTDopUKrSxZAuiQtNT6bgmNWe9D3
Balance___________________________________________ 9999497
ID________________________________________________ ak_XeSuxD8wZ1eDWYu71pWVMJTDopUKrSxZAuiQtNT6bgmNWe9D3
Nonce_____________________________________________ 3
```
#### inspect transaction
```
$ ./aecli inspect th_2kgDHbvFjZn4nRLrxrimzyjdJzdEnMtFnD56r5K5UXHMaMbPkd
BlockHash_________________________________________ mh_2MTsaWUdadr1YRKC5FE7qMHXvtzCZixQyHFV8zsPUCQvwJr2fP
BlockHeight_______________________________________ 151
Hash______________________________________________ th_2kgDHbvFjZn4nRLrxrimzyjdJzdEnMtFnD56r5K5UXHMaMbPkd
 versionField_____________________________________ 1
  Amount__________________________________________ 20000
  Fee_____________________________________________ 1
  Nonce___________________________________________ 1
  Payload_________________________________________ test tranasaction
  RecipientID_____________________________________ ak_2uLM25PWdhrTQfuxgJiM8E5sZREzUoB5iFnukHCz1uAZYBMqwo
  SenderID________________________________________ ak_2a1j2Mk9YSmC1gioUq4PWRm3bsv887MbuRVwyv4KaUGoR1eiKi
```
#### inspect block
```
$ ./aecli inspect mh_2mj6dTVLdRJd2ysvpeMCanMnE816PUjUHZt4N2JBxCbVHb3LnZ
Hash______________________________________________ mh_2mj6dTVLdRJd2ysvpeMCanMnE816PUjUHZt4N2JBxCbVHb3LnZ
Height____________________________________________ 682
PrevHash__________________________________________ kh_Uo54QZNbXAP52BftwHoLVjrfEPmYVn8186D6CfqicXz25gtbE
PrevKeyHash_______________________________________ kh_Uo54QZNbXAP52BftwHoLVjrfEPmYVn8186D6CfqicXz25gtbE
Signature_________________________________________ sg_FctQnGxxCzNUf5vkAfhVVeVAQ8DbBiknQW5Wh6DpSz77ku9tgL23GpaDk6V5yij4Fw1jozNwzJJPYbzMroLkaHJU2rYE3
StateHash_________________________________________ bs_phbFtw7EhFKEP63mtMYd9wSR818VQJqyTqsbLefWJT68ecbR1
Time______________________________________________ 2018-09-20T13:34:51+02:00
TxsHash___________________________________________ bx_GnJ5zjiwAatgQjmQF9gPkFjxKiX7uwvc6z1YGrECSv6QmazeH
Version___________________________________________ 23
  BlockHash_______________________________________ mh_2mj6dTVLdRJd2ysvpeMCanMnE816PUjUHZt4N2JBxCbVHb3LnZ
  BlockHeight_____________________________________ 682
  Hash____________________________________________ th_UvCG8Xo7EvsdA1D21ngLmxnJ1oDYv5qEKKNAg2pDXdYs5mJvW
   versionField___________________________________ 1
    Amount________________________________________ 10000000
    Fee___________________________________________ 1
    Nonce_________________________________________ 61
    Payload_______________________________________ hello Naz! 
    RecipientID___________________________________ ak_XeSuxD8wZ1eDWYu71pWVMJTDopUKrSxZAuiQtNT6bgmNWe9D3
    SenderID______________________________________ ak_2a1j2Mk9YSmC1gioUq4PWRm3bsv887MbuRVwyv4KaUGoR1eiKi
    TTL___________________________________________ 1182
```
## Wallet commands
The wallet commands are those which create and report on key pairs, and all of the operations which require payment:




