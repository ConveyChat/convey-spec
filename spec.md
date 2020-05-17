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

## Message Identifier (MID)

A message identifier is a unique identifier for every message which describes the message type and other specific information. It contains the following parameters:

| _Parameter_     | _Description_                                                                                                 |
| --------------- | ------------------------------------------------------------------------------------------------------------- |
| `MESSAGE_TYPE`  | `p2p` or `d2p` describing if the message is a Peer-to-Peer message or a Dapp-to-Peers broadcast               |
| `MESSAGE_HASH`  | DCAS hash of the message object                                                                               |
| `RECEIVER_TYPE` | Blockchain external account address or contract account address for `p2p` and `d2p` transactions respectively |

**Syntax**

`mm:<MESSAGE_TYPE>:<MESSAGE_HASH>:<RECEIVER_TYPE>`

e.g. `mm:p2p:QmbyizSHLirDfZhms75tdrrdiVkaxKvbcLpXzjB5k34a31:0x9d46038705501f8cb832e5a18492517538b636f3`
e.g. `mm:d2p:QmbyizSHLirDfZhms75tdrrdiVkaxKvbcLpXzjB5k34a31:broadcast#QmbyizSHLirDfZhms75tdrrdiVkaxKvbcLpXzjB5k34a31`

## Message Types

Message Types define the different categories of messages that can be sent.

- P2P (Message type `p2p`)
- D2P (Message type `d2p`)

## Message Object

// TODO: Define `message` in depth

```json
{
  "message": "<b64 encrypted digitally signed message>",
  "timestamp": "<timestamp>"
}
```

## Receiver Types

Receiver Types define the different categories of receivers that messages can be sent to.

- P2P (Receiver type `<address>` e.g. `0x9d46038705501f8cb832e5a18492517538b636f3`)
- D2P (Receiver type `broadcast#<contractAddress>` e.g. `broadcast#QmbyizSHLirDfZhms75tdrrdiVkaxKvbcLpXzjB5k34a31`)

## Messaging Security

// TODO: encrypted using recipient's key

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

- YOu receive a new message id `mm:d2p:whatever:broadcast#ensSmartContract`

- GET /subscriptions from API (http://localhost:3000 OR https://api.convey.chat/ OR https://competitor.api.com)
- if ensSmartContract in subscriptions:
  - parse
- else
  - dont
