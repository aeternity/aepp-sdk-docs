---
layout: page
title: Oracles
---

# Oracles

## Introduction and concepts

Oracles are a way for the blockchain to interact with the outside world, for instance by fetching live data from a website. They are critical for smart contracts, allowing the contract to include real world data.

An oracle has an address, which starts with 'ok$', and may be referred to by an address in the Æternity Naming System. An oracle also has the following attributes:

- An *input format* and an *output format*, neither of which is currently used.
- A *fee* which callers pay to query the oracle
- A *ttl*, expressed either as a *delta* (*n* blocks from now) or as an absolute value for the height of the chain. In either case, the ttl specifies the lifespan of the oracle.

Using the address, a caller can query the oracle, and wait for a response. A query has a *fee* for querying, a *request ttl*, which specifies the timespan in which the oracle must receive the query, and a *response ttl*, specifying how long the caller is willing to wait for the response.

## Operations on oracles

The control flow for an oracle operator is as follows

- register the oracle
- subscribe to the oracle
- answer queries from clients
- possibly extend the lifespan of the oracle, by increasing its ttl
- or expire

and the flow for clients is

- query oracle
- subscribe to the query
- wait for and process the response

## Oracle fees

An oracle can charge a fee of zero or more tokens for its services. This is entirely at the oracle provider's discretion. Other than this, the standard fees for oracle services are as follows:

| Action       |  Basic fee     | TTL fee      |Example
|--------------|----------------|--------------|-----------------------
| Registration |  4             | 1/1000 blocks| ttl of 1000 = 4 + 1000/1000 == 5
| Query        |  2             | 1/1000 blocks| ttl of 20 = 2 + 20/10000 == 3
| Response     |  2             | 1/1000 blocks| ttl of 50 = 2 + 50/10000 == 3


## SDK support for oracles

Currently all features are supported in the SDKs with the exception of ttl extension, which will be released Real Soon Now.

## Sample code

The examples/ directories of the SDKs contain example oracles. In addition here are annotated examples:

[Python sample oracle](Oracle-Python.md)




