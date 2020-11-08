# xdv-any-document-verifiable-protocol
XDV Protocol -  Technology Whitepaper


## V1 - Current

XDV in is current form has a wallet module in Javascript, a VueJS web application and Java Signer. It has a way to store documents
using an append-log protocol on top of Swarm V1.

## V2 - An extensible protocol 

The proposed implementation being worked separates V1 into technology stack features:

- Dart Wallet
- Flutter UI
- Microservices in Go and Node 15
- Solidity Smart Contracts

### Cryptography

- ECDSA, EDDSA, RSA (Legacy)
- SafetyNet, WebAuthn
- BLS, TSS


### Blockchain

- HDWallet
- A new DNS/IPNS/ENS attestation for proof of identity

### Storage

- IPFS
- IPLD

### DID

- XDV schemas
- did-xdv
- Verifiable credentials

## Must haves


1. Allow RSA or EC doc signing, either basic or qualified signing.
2. Must store in decentralized content networks and sign transaction with an  EC  keypair.
3. Must use encryption or ZK signatures to protect privacy data.
4. 
