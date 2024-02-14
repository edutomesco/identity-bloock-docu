# Protocol

With Bloock Identity, developers can empower users to exchange credentials that are securely verified using advanced cryptography and blockchain technology. Tailored for developers, Bloock Identity prioritizes privacy, decentralization, and user data self-sovereignty.

Bloock Identity follows the [Verifiable Credentials Data Model v2.0](https://www.w3.org/TR/vc-data-model-2.0/) standard and [Decentralized Identifiers (DIDs) v1.0](https://www.w3.org/TR/did-core/) standard.

## The basics

### What do we mean by Identity?
An identity can be a person, a company, an organization, a DAO, or a government. Identity can even be a thing: a chair, a room, a bot, and so on. When we talk about identities, we are referring to "identities as accounts".

### What is a claim?
An Identity can provide a claim. You can think of a claim as a statement: something an Identity is saying.

Most of the time, these statements refer to other identities. In other words, **claims usually create relations between identities.**

For example, when a university (identity) says that a student (identity) has a degree, this is a statement (claim) about the student. This statement creates a relation between the student and the university.

### What are the agents in this process?
- **Issuer**: An actor who makes a claim.
- **Holder**: An actor who receives a claim.
- **Verifier**: An actor who verifies if the content of a claim is issued by a specific identity and held by another specific identity.

### And therefore, what is a verifiable credential?
**Credential**: Data that is needed to prove that a claim is issued by a specific identity and held by another specific identity. This data is composed of **a claim and a proof**.

## Decentralized Identifiers (DIDs)

A [DID](https://www.w3.org/TR/did-core/#dfn-decentralized-identifiers) is a simple text string consisting of three parts: 
1. The `did` URI scheme identifier.
2. The identifier for the [DID method](https://www.w3.org/TR/did-core/#dfn-did-methods).
3. The DID method-specific identifier.

![https://cdn.discordapp.com/attachments/1151100469490487307/1206967003500511343/Group_1165.png?ex=65ddee9d&is=65cb799d&hm=ada436c44d4996110fa3241c212b26dfd610a9e94c1d9015600ff9d144708c8e&](https://cdn.discordapp.com/attachments/1151100469490487307/1206967003500511343/Group_1165.png?ex=65ddee9d&is=65cb799d&hm=ada436c44d4996110fa3241c212b26dfd610a9e94c1d9015600ff9d144708c8e&)
Currently in Bloock Identity you can use the following methods.
- [did:polygonid](https://github.com/0xPolygonID/did-polygonid)
- Soon they will be extended...

## did:polygonid

The method id called `did:polygonid` has the following characteristics.
- Is generated from three identity trees and controlled by [Baby JubJub keys](https://docs.iden3.io/publications/pdfs/Baby-Jubjub.pdf). Therefore this key you can create with [Bloock Keys product](reference_to_baby_jub_jub_keys documentation) in a managed way or by yourself locally. It will be very important to be able to control your identity.
- Example:

![https://cdn.discordapp.com/attachments/1151100469490487307/1206965230601506866/Group_1162_1.png?ex=65ddecf7&is=65cb77f7&hm=36a6fdd770f7b18bbf028cbb723b995fdcf2e95f5e2fad8f4fa4d91b4bf6ebec&](https://cdn.discordapp.com/attachments/1151100469490487307/1206965230601506866/Group_1162_1.png?ex=65ddecf7&is=65cb77f7&hm=36a6fdd770f7b18bbf028cbb723b995fdcf2e95f5e2fad8f4fa4d91b4bf6ebec&)
Currently in Bloock Identity we have the following possibilities.
- **did:polygonid:polygon:main**
- Soon they will be extended...

Follows the [Iden3](https://docs.iden3.io/) protocol. The communication protocol between wallets and agents is determined by [DIDComm messaging protocol](https://iden3-communication.io/).


## Core
These are the core components of the Bloock Identity product.

**Diagrama**

### The Issuer
The issuer is an entity (person, organization, or thing) that issues Verifiable Credentials (VCs) to the Holders. VCs are cryptographically signed by the Issuer. Every VC comes from an Issuer.

The role of an issuer on Bloock Identity is to issue digital credentials to users that can be used to prove aspects of their identity and enable various features and actions for users.

#### Resources
- Each issuer generates a DID and therefore a unique and public identifier that represents that identity. `For example: did:polygonid:polygon:main:2qCU58EJgrELSJT6EzT27Rw9DhvwamAdbMLpePztYq`. 
- To create an issuer you need to have a key of type [Baby JubJub (BJJ)](https://docs.iden3.io/publications/pdfs/Baby-Jubjub.pdf), with [Bloock Keys product](reference_to_baby_jub_jub_keys documentation) you can create a managed key where you only need to save its identifier. `For example: 6f36448d-49f3-4b0e-aa72-6e55863302e8`.
> You can also create an identity with your own local key of type BJJ. But then, you will have to maintain it on your own.
- Every issuer must configure how often they want their credentials to be transacted to the blockchain. [Learn more about issuer intervals](go_to_issuer_intervals).

#### Issuer intervals
To understand this section, you must first understand what a [Sparse Merkle Tree Proof](go_to_sparse_merkle_tree_proof) is and how important it is to your business.

When an issuer creates a credential, it will be instantly available synchronously. However, when you create an issuer you will have to choose the transaction interval you want to apply (the cost of use will vary depending on the interval). When we talk about transaction, we talk about transacting your credentials to blockchain and get a proof of integrity of them that is transformed into a verifiable proof called [Sparse Merkle Tree Proof (SMTP)](go_to_sparse_merkle_tree_proof).

We currently offer these intervals.
- 1 minute frequency.
- 5 minute frequency.
- 15 minute frequency.
- 60 minute frequency.

> Example: Let's imagine that you choose a frequency interval of 60 minutes. What it means is that all the credentials created during the last hour (60 minutes), will synchronously run a job that will collect them and execute a transaction on the blockchain. Once the transaction is completed and confirmed, an integrity proof (SMTP) will be automatically generated on all those credentials (each credential will have its own proof). In the case of using a `did:polygonid` issuer the network where the transaction is made is the one marked in the blockchain and network DID, i.e. `did:polygonid:polygon:main` will be transacted over the [polygon blockchain and the mainnet network](https://polygonscan.com/).

### The Verifiable Credential (VC)
The first thing is to be clear that it is a [claim](link_a_what_it_is_a_claim). A credential is a set of one or more claims made by an issuer. 
[Credentials](https://www.w3.org/TR/vc-data-model-2.0/#dfn-credential) might also include an identifier and metadata to describe properties of the credential, such as the validity date and time period, verification material, the revocation mechanism, and so on.
The metadata might be signed by the issuer.
A [Verifiable Credential (VC)](https://www.w3.org/TR/vc-data-model-2.0/#dfn-vc) is a set of tamper-evident claims and metadata that cryptographically prove who issued it.

![a Verifiable
               Credential contains Credential Metadata, Claim(s), and
               Proof(s)](https://www.w3.org/TR/vc-data-model-2.0/diagrams/vc.svg)
            
#### Resources
- In Bloock Identity each credential is identified by a UUID. `For example: 6f36448d-49f3-4b0e-aa72-6e55863302e8`.
- All credentials include a [proof of signature](go_to_proof_signature_explanation), i.e. every credential is signed by its issuer.
- Every credential must reference a schema. [Learn more about schemas](go_to_schema_explanation).
- All credentials include a blockchain integrity proof or [Sparse Merkle Tree Proof (SMTP)](go_to_sparse_merkle_tree_proof) (this proof will be available depending on the [issuer's configuration](go_to_issuer_interval)).

### Schemas
The reusability of credentials across platforms and services is guaranteed by credential schemas.

Bloock Identity use [JSON-LD documents](https://json-ld.org/learn.html) to represent credential schemas.

You must create a schema, which in the end will serve as a template for your credentials, these schemas contain the attributes (claims) that your credentials (VCs) will have. This way, you will be able to reuse your schemas and have more control over the structure of your credentials.

Therefore, to create a credential you must first create a schema and associate it.

These schemas are published in IPFS and therefore generate an id of this type `QmadTvnNKvj2fBDgen35uAp1TfP9pSPVCNeDWw4fitqqne`. This is the identifier of your schema.

### Proofs
Both proofs guarantee that the claim is tamper-resistant.

#### Singature Proof
The claim gets signed by the issuer using his private key. The proof of issuance is the signature itself. This action doesn’t modify the identity state of the issuer, so there’s no on-chain transaction involved.

This proof is always generated synchronously when the credential is created.

#### Sparse Merkle Tree Proof (SMTP)
All the credentials that the issuer creates are stored in a tree structure, specifically in a [Sparse Merkle Tree](https://docs.iden3.io/getting-started/mt/). 

When an identity adds a new claim to his Claims Tree, the root of the tree and, consequently, the identity state change. The process of moving from one state to another is defined using [State Transition](go_to_state_transition_explanation).

##### State Transition
The **issuer states** are published on the blockchain under the identifier, anchoring the state of the issuer with the timestamp when it is published. In this way, the credentials of the issuer can be proved against the anchored issuer state at a certain timestamp. To transition from one state to the other, issuers follow the transition process.

### Revocation
Revocation is the process of invalidating a credential (VC). 
Just as we have a tree structure ([SMT](https://docs.iden3.io/basics/key-concepts/#merkle-trees)) to store issuer credentials, we also store revocations in a separate tree (SMT). These two structures will then mark the actual state of the issuer. 
Therefore, the action of adding the revocation to the revocation tree modifies the root of the revocation tree and, consequently, the identity state.
> The most important thing to keep in mind is that **the revocation will only be effective** at the moment the [issuer's state is transacted on the blockchain](go_to_state_transition_process). So, the effectiveness of the revocation will be marked by the [interval you have defined in the issuer](go_to_interval_documentation).

### The holder
The holder or the user receiving credentials. It is an identity and therefore has its own public DID. It is important that the holder is of the same topology as the issuer that will issue the credential. 
Currently we only accept [did:polygonid](go_to_did:polygonid_docu) issuers and holders.

For example.

- Issuer: `did:polygonid:polygon:main:2qCU58EJgrELSJT6EzT27Rw9DhvwamAdbMLpePztYq`.
- Holder: `did:polygonid:polygon:main:2q544HUegzeRpwr3V2qu9eMwgrAmF5x4E1NCPzbQc4`.

Currently your users will be able to create an identity using the PolygonID wallet, which can be downloaded [here](https://play.google.com/store/apps/details?id=com.polygonid.wallet&hl=en_US). 

Bloock Identity will soon expand support for more [identity wallets](go_to_what_is_wallet_docu).

### What is a wallet?
A digital wallet is an application or software designed to protect and manage identities or holders. A wallet allows you to interact with the issuer when we want to obtain or acquire our credentials and interact with the verifier to share and verify our proofs contained in our credentials.

A wallet is controlled by an identity and therefore must have its own DID. That is why, in most of these wallets when we install the application the identity it's created. That identity will control the wallet. For example, the PolygonID wallet creates an identity like this: `did:polygonid:polygon:main:2q544HUegzeRpwr3V2qu9eMwgrAmF5x4E1NCPzbQc4`.

Each wallet must follow a communication protocol in order to interact with the issuer and the verifier. For example, PolygonID wallet follows the [DIDComm protocol](go_to_did_comm_messaging_docu).

### The verifier
TODO!

### DIDComm messaging
Bloock Identity uses the DIDComm messaging protocol for communication between agents and wallets. The purpose of [DIDComm Messaging](https://identity.foundation/didcomm-messaging/spec/) is to provide a secure, private communication methodology built atop the decentralized design of [DIDs](https://www.w3.org/TR/did-core/). We use this protocol with the [Iden3comm](https://iden3-communication.io/). 

## Understand the flow
Let's describe how an end-to-end flow works to see how all the terms described above relate to each other.

### Create BJJ key
In order to create an identity in Bloock Identity I will first need to create or have a Baby JubJub (BJJ) key. This key will be very important to have it saved because it will be used to control our issuer.

I have two options to get this key.
1. You can create a BJJ key with our managed key product ([Bloock Keys product](go_to_keys_documentation)), your key will be identified by a UUID. This identifier will be enough to control your issuer.
`Example: 6f36448d-49f3-4b0e-aa72-6e55863302e8`
2. If you have created a BJJ type key locally, i.e. you are aware of its private key, then you can use it to control your issuer.
`Example: bf5e13dd8d9f784aee781b4de7836caa3499168514553eaa3d892911ad3c345j`

### Create the issuer
Once we have our key available, we will create the issuer.  
Before creating the issuer we should think about how often we want the status of our issuer to be transacted. [Here](go_to_intervals_documentation) you can see what intervals we have available. If you need information to make this decision you can contact us. For this example, let's imagine that I choose a 60-minute interval.

Once we have our issuer we can see its identity represented with its [DID](go_to_DIDs_identifier) (decentralized identifier). This is unique and totally public, this DID is directly related to the key you have created previously.
`Example: did:polygonid:polygon:main:2qCU58EJgrELSJT6EzT27Rw9DhvwamAdbMLpePztYq`

### Create the schema
Next, we must think about what type of credentials we want to issue. For example, we want to issue a card that identifies Bloock employees. In order to create the schema I have to follow these steps.
1. I must first think about the name of the schema type, in this case for example it would be BloockEmployee.
2. I must define what attributes my credential will have, for example, I will put an employee number, name and date of birth.

Once this is defined, I will be able to create my schema. Notice that all we are doing is defining the attributes that our credentials will have.

[The schemas](go_tio_schemas_documentation) are uploaded to IPFS, in order to identify the schemas we use their IPFS identifier.
`Example: QmadTvnNKvj2fBDgen35uAp1TfP9pSPVCNeDWw4fitqqne`

### Create the credential
To create a credential, we will need two very important things.
1. I need the schema identifier that it will reference, which will therefore mark which attribute structure it will have. In my case it will be my employee number, name and date of birth.
2. I will need the BJJ key created for that issuer, because when we create a credential let's remember that in order to be verifiable we need to be able to sign it and get a proof of authenticity.
3. You should know who is going to be the holder of this credential or rather which is the user who is going to receive this credential. This user must have created his own identity at the same time. For example, in the case of our employee for whom we are going to issue this credential, the following DID identifies him/her: `did:polygonid:polygon:main:2q544HUegzeRpwr3V2qu9eMwgrAmF5x4E1NCPzbQc4`.
4. We will also be able to add additional metadata such as expiration date, version number, etc...

Once the credential is created we will obtain a UUID identifier.
`Example: 0e3199ac-8147-4c7a-938b-d33f9107dace`

The most important thing is that this credential is already a [Verifiable Credential (VC)](go_to_verifiable_credential_docu) because it already includes a signature proof, and therefore, this credential would already be valid to be verified by any verifier.

But Bloock Identity's product offers a second test, related to integrity in blockchain.
The [Sparse Merkle Tree proof](go_to_sparse_merkle_tree_proof) is a proof that will be available depending on the [interval time](go_to_interval_issuer_documentation) you have chosen and is related to the issuer's state. 
As I have previously chosen a 60 minutes interval, it means that I will have my SMTP proof available after ~60 minutes.

### Credential offering
The credential offering process refers to the transfer of the Verifiable Credential (VC) to the assigned user or holder. 
It requires two agents (issuer and holder) and a [wallet or software](go_to_what_is_a_wallet_docu) where the credential will be stored. 
At the user level, this is done by scanning a QR code generated by the issuer from the user's wallet. 
At the protocol level this communication is highly secure thanks to the [DIDComm protocol](go_to_did_comm_communication) used and the authentication and identity proofs mechanisms.

Therefore, to execute the offering.
1. The issuer generates a request QR code.
2. The user autonomously scans this QR code with his credential management application or wallet.
3. The user authenticates and verifies his identity to the issuer, who, once approved, sends him the Verifiable Credential.

### Verify the credential
TODO!

### Revoke the credential
TODO!

