---
layout: page
title: The Æternity Naming System
---

# The Æternity Naming System (AENS)

## Introduction

AENS provides a mapping from human-readable names, such as `example.aet` to account addresses (starting with `ak$` or oracle addresses (starting with `ok$`). It has been designed to work in the zero-trust blockchain environment, with features designed to prevent malicious nodes from stealing addresses clients have asked to register. 

AENS addresses, like DNS addresses, contain 1 or more parts selected by clients, separated by the `.` character.

The [full documentation](https://github.com/aeternity/protocol/blob/master/AENS.md) of the AENS is the canonical source of information about its operation.

## Registering and working with names

The general procedure for registering AENS names is this:

- the client makes a hash of the name, and a secret salt
- the client *pre-claims* this name with the blockchain.
- when the pre-claim has been written into the blockchain the client can issue a *claim* transaction to take the name
- the name is taken for as many blocks as the client has registered it, or until the client *revokes* the name
- the client can *transfer* the name at any time before its expiration
- the owner of a registered name can associate it with either an account or an oracle address.

## Python SDK support

Literally could not be simpler:

```
from aeternity.aens import AEName
from aeternity.config import Config

Config.set_default(Config(local_port=3013, internal_port=3113, websocket_port=3114))

name = AEName('foobar.aet')
if name.is_available():
    name.preclaim()
    name.claim_blocking()
    name.update(target='ak$deadbeef')
```
