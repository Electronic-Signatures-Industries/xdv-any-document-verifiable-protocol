# xdv-any-document-verifiable-protocol
XDV Protocol -  Technology Whitepaper


## V1 - Current

XDV in is current form has a wallet module in Javascript, a VueJS web application and Java Signer. It has a way to store documents
using an append-log protocol on top of Swarm V1.

## V2 - Smart Contracts and did

### Content storage

Must be dual or pluggable, uses both IPFS and Swarm Bee. Protocol for storing objects contains  :

- An XDV index.json - JSON Schema
- An updated DID
- An updated DDoc

#### XDV JSON Schema

```js
{
    epoch: 0,
    timestamp: 18521596,
    did: 'did.json',
    ddoc: 'refs.json',
    sig: '...',
    hash:'....'
}
```

**epoch**: current  epoch from smart contract
**timestamp**: current time from smart contract
**did**: current did
**ddoc**: current did doc



#### XDV DID Doc JSON Schema

```js
{
    documentTransactions: {
        ref: 'cid',
        hash,
        sig,
        algorithm,
        length,
        contentType,
        scopes,
        sigSpec,
        created,
        lastModified,
        isAnon,
        isMultisig,
        signedWithDID,
    }
}
```
Each document transaction has:

**ref**: cid
**hash**: document hash
**sig**: document signature
**algorithm**: algorithm used
**length**: length in bytes
**contentType**: content type
**scopes**: roles / acls
**sigSpec**
**isAnon**: contains anon creds sig
**isMultisig**: has been signed with multisig
**signedWithDID**: did reference
**lastModified**
**created**


Folder structure

- index.json
- did.json
- doc.json
- index.html

#### XDV Index Presentation

index.html contains a single page application which renders a XDV document sig package 

#### DID

XDV DID module uses a RSA sig generated from ACME Let's Encrypt API creating a PKCS#12 with Chain of Trust with a KYC on top to validate Proof of Residency. This allows XDV PKCS Signature Application client to work both with Smart Cards and Portable PKCS signatures in the form of .p12 files. An existing testnet API can be accessed in https://app.xdv.digital/p12

Additional DID signatures in Ed25519 and ECDSA / secp256k1 are also attached

### Smart Contracts

XDV uses a light version of MDV contracts for workflows

### ExternalAdapterRegistry

### RoutingRegistry

### ABIWorkflows

### SmartRouter


An **adapter** is a job to be executed, once a **event lifecycle pipeline like ABIWorkflow** steps thru each state, with the next step being **a registered route**

Create Job
    |
Execute **adapter**  -- **event lifecycle** [before - mount - after - next] -- **route**

## Copyright  Nov  2020 // Rogelio Morrell IFESA
