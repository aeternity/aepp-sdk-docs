# Our networks, and how to use them

## Introduction

### sdk-testnet sdk-edgenet, uat-testnet

 We (the SDK team) currently run two networks, sdk-testnet and sdk-edgenet. Testnet is the latest stable release, and Edgenet is the next. At the time of writing, testnet is at epoch verson 0.24.0 and edgenet is at version 0.25.0 of Epoch.
 
The æternity core team run another network, testnet. It's for their testing and is not guaranteed to work with our SDKs. But it's the one which has the very latest features and may well be useful for you if you are an exotic creature who runs their own nodes or something else.

If you download from package managers, you’ll automatically connect to testnet. If you clone the repository, you’ll connect to edgenet. If you run your own nodes, you can use whatever version you like, of course.

Guide to version numbers

```
0.24.0-0.2.0 - Universal Flavor & Improved RPC
^^^^^^ ^^^^^^^^ 
|      |
|      SDK version (next would be 0.24.0-0.3.0)
epoch version
```


### sdk-testnet

audience -- people using released versions of our SDKs (github releases or npm/yarn default install). Most software developers should use this one.

contracts.aepps.com talks to this one


### sdk-edgenet

audience -- people developing the SDKs, developers who need the latest features from the develop branch on github. This network is used primarily for development and can be reset without notification.

If you clone one of our repos from the default branch (develop) you will connect to edgenet automatically. 

### testnet

audience -- core developers, miners, people who want to track the bleeding edge. You may not be able to connect to this using our SDKs because it's a version later than the ones they support.

## Getting tokens


There are two ways of getting tokens. The faucets operated by the SDK team will give you tokens for no effort at all, or you can mine your own, which is obviously coolers. The SDK team does not provide tokens for the uat-testnet via a faucet.

### Faucets

sdk-testnet https://faucet.aepps.com/
sdk-edgenet https://edge-faucet.aepps.com/

### Mining

The simplest way of doing this is using docker.

Firstly determine the version of Epoch you need using the `/v2/status` endpoint. Example output on edgenet:

```javascript=
// 20181109160745
// https://sdk-edgenet.aepps.com/v2/status

{
  "difficulty": 2017450664,
  "genesis_key_block_hash": "kh_2D3fMvkjuNaDwsrTctR4DjWUzztys8b1NBQrQYedTgCvZSkGpJ",
  "listening": true,
  "node_revision": "765f9cc0fb0904adb4efd0acfecd3c78c0d570f3",
  "node_version": "0.25.0",
  "peer_count": 0,
  "pending_transactions_count": 0,
  "protocols": Array[1][
    {
      "effective_at_height": 0,
      "version": 28
    }
  ],
  "solutions": 0,
  "syncing": true
}
```

the `node_version` field tells you this is version 0.25.0

Now you need to make a config file. The current versions of testnet and edgenet are versions 0.24.0 and 0.25.0 and appropriate config files for these are given next. Later versions of Epoch will almost certainly have different formats, so bear this in mind.

Create a file `myepoch.yaml`, with contents

v0.24.0
```yaml
---
peers:
  - aenode://pp_HdcpgTX2C1aZ5sjGGysFEuup67K9XiFsWqSPJs4RahEcSyF7X@sync.sdk-testnet.aepps.com:3015

keys:
    password: "top secret"
    dir: ./keys

chain:
    persist: true

mining:
    autostart: true
    beneficiary: "ak_2iBPH7HUz3cSDVEUWiHg76MZJ6tZooVNBmmxcgVK6VV8KAE688"
    cuckoo:
         miner:
             executable: mean16s-generic
             extra_args: ""
             node_bits: 16

```

v0.25.0
```yaml
---
peers:
  - aenode://pp_HdcpgTX2C1aZ5sjGGysFEuup67K9XiFsWqSPJs4RahEcSyF7X@sync.sdk-edgenet.aepps.com:3015

keys:
    peer_password: "top secret"
    dir: ./keys

chain:
    persist: true

mining:
    autostart: true
    beneficiary: "ak_2iBPH7HUz3cSDVEUWiHg76MZJ6tZooVNBmmxcgVK6VV8KAE688"
    cuckoo:
         miner:
             executable: mean16s-generic
             extra_args: ""
             node_bits: 16
```

replace `ak_2iBPH7HUz3cSDVEUWiHg76MZJ6tZooVNBmmxcgVK6VV8KAE688` with the public key to a wallet you control, unless you wish to donate your mining proceeds to the SDK team (strongly encouraged).

Also note that we use a different miner on our test networks--we use one which is less compute intensive, since we're not running a full, secure blockchain.

Now you can run it with a command similar to this
```shell
docker run \ 
    -p 3013:3013 \
    -v $PWD/myepoch.yaml:/home/epoch/myepoch.yaml \   
    -e EPOCH_CONFIG=/home/epoch/myepoch.yaml \
     aeternity/epoch:vXX.Y.Z
```
replace `$PWD/mypoch.yaml` with the path to the file you created, and XX.YY.Z with the version, i.e. 0.24.0 (currently) for testnet, 0.25.0 (at time of writing) for edgenet. These will of course change.

If all is well you should see output similar to this
```
15:17:29.362 [info] TX-pool sync requries getting 0 TXs
15:17:29.757 [info] TX-pool sync added 0 TXs
15:17:30.212 [info] TX-pool synchronization finished!
15:17:42.344 [info] Synced blocks 1 - 1
15:17:50.976 [info] Synced blocks 2 - 35
15:17:51.775 [info] Synced blocks 36 - 96
15:17:52.009 [info] Synced blocks 97 - 100
```
