# Convey Chat Messaging Protocol Specification

This specification describes the Convey Chat messaging protocol, which can be used with any decentralized ledger system which has the concept of addresses, to create an interoperable messaging network. Implementations of the protocol can be uniquely designed based on their underlying decentralized ledger.

## Overview

Blockchains and the rise of dApps have introduced new problems around communication. Consider the example of buying a domain. Traditionally, buying a domain involves entering your email address and/or phone number, allowing the registrar to contact you when the domain is about to expire. However, in the case of something like ENS, where the dApp owners only know the buyer's Ethereum address and nothing else, sending a renewal reminder is not possible with the current technology being used.

By implementing fully decentralized address based messaging, two major use case areas are enabled

- dApp to Peer (D2P) communication - e.g. renewal reminders from ENS
- Peer to Peer (P2P) communication - e.g. discussing an NFT trade

## Glossary

| _Term_                   | _Definition_                                                                                          |
| ------------------------ | ----------------------------------------------------------------------------------------------------- |
| Sender                   | The address creating the blockchain transaction to send a message                                     |
| Receiver                 | Address included as a recipient of a message                                                          |
| DCAS                     | Decentralized Content Addressable Storage e.g. IPFS                                                   |
| Message                  | Data being sent to one or multiple receivers                                                          |
| Message Hash             | The DCAS hash returned for the message object                                                         |
| Message Identifier (MID) | A unique identifier for every message which describes the message type and other specific information |
| Message Object           | The data structure representing a message                                                             |

## Protocol Configuration

## Message Identifier (MID)

A message identifier is a unique identifier for every message which describes the message type and other specific information. It uses the following syntax

`mm:<message type>:<message hash>:<receiver type>`

// TODO: `receiver type` needs to be better defined for message types which are not P2P

e.g. `mm:p2p:QmbyizSHLirDfZhms75tdrrdiVkaxKvbcLpXzjB5k34a31:0x9d46038705501f8cb832e5a18492517538b636f3`

## Message Unique Suffix

A messaging unique suffix is the unique portion of a message which identifies it's message type.
e.g. The messaging unique suffix of P2P text message would be `mm:p2p:`

## Message Types

## Message Object

## Messaging Security

## Lifecycle

## Anti-Spam Protections

## REST API
