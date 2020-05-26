# Convey

**Version**: v0.0.2
**Editors**:

- [Haardik](https://www.linkedin.com/in/haardikkk/)

**Contributors**:

---

This specification describes the Convey Chat messaging protocol, which can be used with any decentralized ledger system which has the concept of addresses, to create an interoperable messaging network. Implementations of the protocol can be uniquely designed based on their underlying decentralized ledger.

## Overview

Blockchains and the rise of dApps have introduced new problems around communication. Consider the example of buying a domain. Traditionally, buying a domain involves entering your email address and/or phone number, allowing the registrar to contact you when the domain is about to expire. However, in the case of something like ENS, where the dApp owners only know the buyer's Ethereum address and nothing else, sending a renewal reminder is not possible with the current technology being used.

By implementing fully decentralized address based messaging, two major use case areas are enabled

- dApp to Peer(s) (D2P) communication - e.g. renewal reminders from ENS, community announcements
- Peer to Peer (P2P) communication - e.g. discussing an NFT trade

Convey is not an Ethereum-specific protocol, but can be used across various decentralized ledgers to create cross-blockchain communication platforms.

## Glossary

| _Term_                   | _Definition_                                                                                          |
| ------------------------ | ----------------------------------------------------------------------------------------------------- |
| Sender                   | The address creating the blockchain transaction to send a message                                     |
| Receiver                 | Address included as a recipient of a message                                                          |
| DCAS                     | Decentralized Content Addressable Storage e.g. IPFS                                                   |
| Transaction              | A blockchain transaction that published the Message Identifier to the chain                           |
| Message                  | Data being sent to one or multiple receivers                                                          |
| Message Hash             | The DCAS hash returned for the message object                                                         |
| Message Identifier (MID) | A unique identifier for every message which describes the message type and other specific information |
| Message Object           | The data structure representing a message                                                             |
| Blockchain Identifier    | A string representation of a blockchain and network e.g. `ethereum@ropsten`, `algorand@testnet`       |

## Message Identifier (MID)

A message identifier is a unique identifier for every message which describes the message type and other specific information. It contains the following parameters:

| _Parameter_             | _Description_                                           |
| ----------------------- | ------------------------------------------------------- |
| `MESSAGE_HASH`          | DCAS hash of the message object                         |
| `RECEIVER_TYPE`         | Blockchain external account address or contract address |
| `BLOCKCHAIN_IDENTIFIER` | Blockchain identifier for the receiver type             |

**Syntax**

`mid:<MESSAGE_HASH>:<RECEIVER_TYPE>:<BLOCKCHAIN_IDENTIFIER>`

e.g. `mid:QmbyizSHLirDfZhms75tdrrdiVkaxKvbcLpXzjB5k34a31:0x9d46038705501f8cb832e5a18492517538b636f3:ethereum@ropsten`
e.g. `mid:QmbyizSHLirDfZhms75tdrrdiVkaxKvbcLpXzjB5k34a31:broadcast#0xd0a6E6C54DbC68Db5db3A091B171A77407Ff7ccf:ethereum@mainnet`

## Message Hash

A message hash is the hash returned from the DCAS when you upload the Message Object.

E.g. In the case of IPFS, it will look something like `QmbyizSHLirDfZhms75tdrrdiVkaxKvbcLpXzjB5k34a31`

## Receiver Types

Receiver Types define the different categories of receivers that messages can be sent to.

- P2P (Receiver type `<address>` e.g. `0x9d46038705501f8cb832e5a18492517538b636f3`)
- D2P (Receiver type `broadcast#<contractAddress>` e.g. `broadcast#QmbyizSHLirDfZhms75tdrrdiVkaxKvbcLpXzjB5k34a31`)

## Blockchain Identifier

A blockchain identifier is used to specify what blockchain and network the sender and receivers are using. It is represented by the `<blockchain name> + @ + <network name>`

E.g. `ethereum@ropsten` , `algorand@testnet`

## Message Object

The message object is what gets uploaded to the CAS and it's hash is put on chain. It has the following syntax

```json
{
  "payload": "<compressed encrypted digitally signed message>",
  "timestamp": "<timestamp>"
}
```

where `payload` is a string representation of the following **Intermediate Message Object** encrypted with the receiver's public key and then compressed

```json
{
  "message": {
    "body": {
      "title": "<message title>",
      "text": "<text message>",
      "image": "<image base64 data>",
      "html": "<html message>"
    },
    "sender": {
      "address": "<sender address>",
      "blockchainIdentifier": "<blockchain identifier>"
    }
  },
  "signature": "<signed message with sender private key>"
}
```

## Messaging Security

1. An intermediate message object is generated from the client application
2. The intermediate message object is signed using the sender's private key and the `signature` is added as a property to the message object
3. The new message object is encrypted with the receiver's public key
4. The encrypted message object is compressed and converted to a string
5. A message object is generated with the payload being the encrypted compressed string along with a unix timestamp
6. The message object is uploaded to the DCAS and a blockchain transaction is made to anchor the hash on chain as a Message Identifier
7. Reciever client listener will parse the message, and decrypt it using their private key
8. Receiver client will verify signature to ensure it's coming from the correct sender

## Lifecycle

TODO:

sender convey client > ipfs > blockchain > receiver convey client

## Anti-Spam Protections

// TODO: blacklist

## REST API Backend

// TODO: subscriptions

Backend - Open Source

- Run it locally
- OR, you can use our hosted version
- NOTE: Third parties are free to host our API and provide it as a service

Metamask, Trust Wallet, Argent Wallet (Integrated with Convey)

- "Convey API URL" - http://localhost:3000 OR https://api.convey.chat/ OR https://competitor.api.com

- YOu receive a new message id `mid:d2p:whatever:broadcast#ensSmartContract`

- GET /subscriptions from API (http://localhost:3000 OR https://api.convey.chat/ OR https://competitor.api.com)
- if ensSmartContract in subscriptions:
  - parse
- else
  - dont
