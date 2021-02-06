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

mapActions tx
mapGetters queries

DR, PACIENTE, FARMACIA

0, EMITE RECETA -> PACIENTE RECIBE
1, PACIENTE ADQUIERE USANDO RECETA -> FARMACIA VERIFIES CREDENTIALS
FORK
1, 2, Y) FARMACIA VENDE MEDICAMENTOS -> ENVIADO A PACIENTE
1, 3,N) DENEGADO POR CREDENCIAL INVALIDO -> PACIENTE NOTIFICADO
3, 0

### WStateRelayer

Contrato se encarga de relay el mensaje a la direccion que escucha eventos registrados por un topico especifico.

### WAction

El WStateRelayer envia mensaje a un topico, este topico ejecuta un accion definida en el mensaje.

### WMutation

Cada accion emite eventos, cuales son capturados por instancias de WMutation, el cual modifica el estado ya se en cadena (on chain) o fuera de cadena (off chain). Ejemplo: Se requiere modificar y actualizar con el hash mas reciente, el contenido de un documento IPLD.

### ExternalAdapterRegistry

Adicionalmente, una accion puede ser pura, es decir, una funcion pura netamente ejecutada en el blockchain, o una accion hibridad por medio de el adaptor de registro externo, cual puede ser un oraculo, un mensaje a un servicio centralizado u otro contrato externo (external call).


## Configuracion

1. Crear las acciones y registrarar en registro
2. Crear los escuchas / listener para aplicar mutaciones.

## Secuencia


1. `Aplicacion ejecuta secuencia #1`: Crear receta - call recetas.execute(...)
2. `Relayer obtiene y reenvia al contrato de accion`: relayer lee mapping y ejecuta accion
3. `Accion envia resultados a mutacion`: Accion aplica regla de negocios y emite evento


## Copyright  Nov  2020 // Rogelio Morrell IFESA
