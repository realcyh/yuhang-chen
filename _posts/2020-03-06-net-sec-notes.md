---
layout: post
title: Network Security
date: 2020-03-06
Author: realcyh
toc: true
tags: [notes]
--- 

## Symmetric Cryptography

### Symmetric key cryptography

Bob and Alice share the same(symmetric) key.

Q: How do they agree on key value? 

A: They can use other ways to transport the key, like hand to each other by hand or use a public key to encrypt the symmetric key and send it through internet.

* Stream cipher: Encrypt on bit at a time.
* Block cipher: Break plaintext into equal-size blocks and encrpt one block as a unit.
![img](https://imgur.com/0Xyk7su)

## Protocol Security
 
### Network Overview

#### Network protocol

A network protocol defines the rules and conventions for communication between network devices.

Protocols can be broadly classified as connectionless and connection oriented.

* Connection-less network protocols

  Sends data out as soon as there is enough data to be transmitted.

  E.g., user datagram protocol (UDP).

* Connection-oriented network protocols

  Provides a reliable connection stream between two nodes.

  Consists of set up, transmission, and tear down phases.

  Creates virtual circuit-switched network.

  E.g., transmission control protocol (TCP).

#### Network Layers

* OSI Model

* TCP/IP Model



