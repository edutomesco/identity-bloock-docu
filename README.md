# Protocol

With BLOOCK Identity, developers can empower users to exchange credentials that are securely verified using advanced cryptography and blockchain technology. Tailored for developers, BLOOCK Identity prioritizes privacy, decentralization, and user data self-sovereignty.

The protocol used by BLOOCK Identity is standarized under the [Verifiable Credentials Data Model v2.0](https://www.w3.org/TR/vc-data-model-2.0/) and [Decentralized Identifiers (DIDs) v1.0](https://www.w3.org/TR/did-core/) standards, both from developed by the [World Wide Web Consortium (W3C)](https://www.w3.org/).

## The basics

### What do we mean by Identity?
An identity can be a person, a company, an organization, an entity, or a government. Identity can even be a thing: a chair, a room, a bot, and so on. When we talk about identities, we are referring to "identities as accounts".

### What is a claim?
An Identity can provide a claim. You can think of a claim as a statement: something an Identity is saying.

Most of the time, these statements refer to other identities. In other words, **claims usually create relations between identities.**

For example, when a university (identity) says that a student (identity) has a degree, this is a statement (claim) about the student. In this case, this statement creates a relation between the two identities, the student (also referred as Holder) and the university (also referred as Issuer).

### What are the agents in this process?
- **Issuer**: An identity who makes a claim.
- **Holder**: An identity who receives a claim.
- **Verifier**: An identity who verifies if the content of a claim is issued by a specific identity and held by another specific identity.

![https://cdn.discordapp.com/attachments/1151100469490487307/1210140212773130310/Group_1324_4.png?ex=65e979e6&is=65d704e6&hm=4ebd8911ec2562a229d5f3b77da35f078298b7f295c72abdf963254f984aecf4&](https://cdn.discordapp.com/attachments/1151100469490487307/1210140212773130310/Group_1324_4.png?ex=65e979e6&is=65d704e6&hm=4ebd8911ec2562a229d5f3b77da35f078298b7f295c72abdf963254f984aecf4&)
### And therefore, what is a Verifiable Credential?
A **Verifiable Credential (VC)** is the set of data that represents the statement made from an Issuer to a Holder and information needed to make this statement verifiable.  
It usually contains:

-   Information to identify the Issuer
-   Information to identify the Holder
-   The credential type or schema
-   The attributes or properties being asserted by the Issuer
-   Evidences that can be used to verify the integrity and/or authenticity of the credential
-   Other information such as validity period, terms, ...

## Decentralized Identifiers (DIDs)
The [Decentralized Identifiers (DIDs)](https://www.w3.org/TR/did-core/#dfn-decentralized-identifiers) are a new type of globally unique identifier. They are designed to enable individuals and organizations to generate their own identifiers using systems they trust. These new identifiers enable entities to prove control over them by authenticating using cryptographic proofs such as digital signatures.

A [DID](https://www.w3.org/TR/did-core/#dfn-decentralized-identifiers) is a simple text string consisting of three parts: 
1. The `did` URI scheme identifier.
2. The identifier for the [DID method](https://www.w3.org/TR/did-core/#dfn-did-methods).
3. The DID method-specific identifier.

![https://cdn.discordapp.com/attachments/1151100469490487307/1206967003500511343/Group_1165.png?ex=65ddee9d&is=65cb799d&hm=ada436c44d4996110fa3241c212b26dfd610a9e94c1d9015600ff9d144708c8e&](https://cdn.discordapp.com/attachments/1151100469490487307/1206967003500511343/Group_1165.png?ex=65ddee9d&is=65cb799d&hm=ada436c44d4996110fa3241c212b26dfd610a9e94c1d9015600ff9d144708c8e&)
Currently in BLOOCK Identity only supports the method **did:polygonid**, but it's expected to add more in the future.
- [did:polygonid](https://github.com/0xPolygonID/did-polygonid)
- Soon they will be extended...

## did:polygonid

The method id called `did:polygonid` has the following characteristics.
- It's derived from a [Baby JubJub key](https://docs.iden3.io/publications/pdfs/Baby-Jubjub.pdf) and other cryptographic material. This key can be created with [BLOOCK Keys product](go_to_baby_jub_jub_keys_documentation) in a managed way or by yourself locally. It will be very important to be able to control your identity.
- [Here](https://github.com/iden3/go-iden3-crypto/tree/master/babyjub) you will find more technical information about the key creation.

- Example:

![https://cdn.discordapp.com/attachments/1151100469490487307/1206965230601506866/Group_1162_1.png?ex=65ddecf7&is=65cb77f7&hm=36a6fdd770f7b18bbf028cbb723b995fdcf2e95f5e2fad8f4fa4d91b4bf6ebec&](https://cdn.discordapp.com/attachments/1151100469490487307/1206965230601506866/Group_1162_1.png?ex=65ddecf7&is=65cb77f7&hm=36a6fdd770f7b18bbf028cbb723b995fdcf2e95f5e2fad8f4fa4d91b4bf6ebec&)
Currently in BLOOCK Identity we have the following possibilities.
- **did:polygonid:polygon:main**
- Soon they will be extended...

Follows the [Iden3](https://docs.iden3.io/) protocol. The communication protocol between wallets and agents is determined by [DIDComm messaging protocol](https://iden3-communication.io/).


## Core
These are the core components of the BLOOCK Identity product.

### The Issuer
The Issuer is an entity (person, organization, or thing) that issues Verifiable Credentials (VCs) to the Holders. VCs are cryptographically signed by the Issuer. Every VC comes from an Issuer.

The role of an Issuer on BLOOCK Identity is to issue digital credentials to users that can be used to prove aspects of their identity and enable various features and actions for users.

#### The Issuer in BLOOCK...
- Each Issuer generates a DID and therefore a unique and public identifier that represents that identity. `For example: did:polygonid:polygon:main:2qCU58EJgrELSJT6EzT27Rw9DhvwamAdbMLpePztYq`. 
- To create an Issuer you need to have a key of type [Baby JubJub (BJJ)](https://docs.iden3.io/publications/pdfs/Baby-Jubjub.pdf), with [BLOOCK Keys product](go_to_baby_jub_jub_keys_documentation) you can create a managed key where you only need to save its identifier. `For example: 6f36448d-49f3-4b0e-aa72-6e55863302e8`.
> You can also create an identity with your own local key of type BJJ. But then, you will have to maintain it on your own.
- Every Issuer must configure how often they want their credentials to be transacted to the blockchain. [Learn more about Issuer intervals](#issuer-intervals).

#### Issuer intervals
To understand this section, you must first understand what a [Sparse Merkle Tree Proof](#sparse-merkle-tree-proof-(SMTP)) is and how important it is to your business.

When an Issuer creates a credential, it will be instantly available synchronously. However, when you create an Issuer you will have to choose the transaction interval you want to apply (the cost of use will vary depending on the interval). When we talk about transaction, we talk about transacting your credentials to blockchain and get a proof of integrity of them that is transformed into a verifiable proof called [Sparse Merkle Tree Proof (SMTP)](#sparse-merkle-tree-proof-(SMTP)).

We currently offer these intervals.
- 1 minute frequency.
- 5 minute frequency.
- 15 minute frequency.
- 60 minute frequency.

> Example: Let's imagine that you choose a frequency interval of 60 minutes. What it means is that all the credentials created during the last hour (60 minutes), will asynchronously run a job that will collect them and execute a transaction on the blockchain. Once the transaction is completed and confirmed, an integrity proof (SMTP) will be automatically generated on all those credentials (each credential will have its own proof). In the case of using a `did:polygonid` Issuer the network where the transaction is made is the one marked in the blockchain and network DID, i.e. `did:polygonid:polygon:main` will be transacted over the [polygon blockchain and the mainnet network](https://polygonscan.com/).

### The Verifiable Credential (VC)
The first thing is to be clear what a [claim](#what-is-a-claim?) is. A credential is a set of one or more claims made by an Issuer. 
[Credentials](https://www.w3.org/TR/vc-data-model-2.0/#dfn-credential) might also include an identifier and metadata to describe properties of the credential, such as the validity date and time period, verification material, the revocation mechanism, and so on.
The metadata might be signed by the Issuer.
A [Verifiable Credential (VC)](https://www.w3.org/TR/vc-data-model-2.0/#dfn-vc) is a set of tamper-evident claims and metadata that cryptographically prove who issued it.

![https://cdn.discordapp.com/attachments/1151100469490487307/1207640880496906271/Group_1325.png?ex=65e06236&is=65cded36&hm=37f9f2c8351494ea9014baaa4418cc82808315165a65128e2f831aa376856d9f&](https://cdn.discordapp.com/attachments/1151100469490487307/1207640880496906271/Group_1325.png?ex=65e06236&is=65cded36&hm=37f9f2c8351494ea9014baaa4418cc82808315165a65128e2f831aa376856d9f&)       
#### Verifiable Credential in BLOOCK...
- In BLOOCK Identity each credential is identified by a UUID. `For example: 6f36448d-49f3-4b0e-aa72-6e55863302e8`.
- All credentials include a [proof of signature](#signature-proof), i.e. every credential is signed by its Issuer.
- Every credential must reference a schema. [Learn more about schemas](#schemas).
- All credentials include a blockchain integrity proof or [Sparse Merkle Tree Proof (SMTP)](#sparse-merkle-tree-proof-(SMTP)) (this proof will be available depending on the [Issuer's configuration](#issuer-intervals)).

### Schemas
The reusability of credentials across platforms and services is guaranteed by credential schemas.

BLOOCK Identity use [JSON-LD documents](https://json-ld.org/learn.html) to represent credential schemas.

You must create a schema, which in the end will serve as a template for your credentials, these schemas contain the attributes (claims) that your credentials (VCs) will have. This way, you will be able to reuse your schemas and have more control over the structure of your credentials.

Therefore, to create a credential you must first create a schema and associate it.

These schemas are published in IPFS and therefore generate an id of this type `QmadTvnNKvj2fBDgen35uAp1TfP9pSPVCNeDWw4fitqqne`. This is the identifier of your schema.

### Proofs
Both proofs guarantee that the claim is tamper-resistant.

#### Singature Proof
The claim gets signed by the Issuer using his private key. The proof of issuance is the signature itself. This action doesn’t modify the identity state of the Issuer, so there’s no on-chain transaction involved.

This proof is always generated synchronously when the credential is created.

#### Sparse Merkle Tree Proof (SMTP)
All the credentials that the Issuer creates are stored in a tree structure, specifically in a [Sparse Merkle Tree](https://docs.iden3.io/getting-started/mt/). 

When an identity adds a new claim to his Claims Tree, the root of the tree and, consequently, the identity state change. The process of moving from one state to another is defined using [State Transition](#state-transition).

##### State Transition
The **Issuer states** are published on the blockchain under the identifier, anchoring the state of the Issuer with the timestamp when it is published. In this way, the credentials of the Issuer can be proved against the anchored Issuer state at a certain timestamp. To transition from one state to the other, issuers follow the transition process.

### Revocation
Revocation is the process of invalidating a credential (VC). 
Just as we have a tree structure ([SMT](https://docs.iden3.io/basics/key-concepts/#merkle-trees)) to store Issuer credentials, we also store revocations in a separate tree (SMT). These two structures will then mark the actual state of the Issuer. 
Therefore, the action of adding the revocation to the revocation tree modifies the root of the revocation tree and, consequently, the identity state.
> The most important thing to keep in mind is that **the revocation will only be effective** at the moment the [Issuer's state is transacted on the blockchain](#state-transition). So, the effectiveness of the revocation will be marked by the [interval you have defined in the Issuer](#issuer-intervals).

### The Holder
The Holder or the user receiving credentials. It is an identity and therefore has its own public [DID](#decentralized-identifiers-(DIDs)). It is important that the Holder is of the same topology as the Issuer that will issue the credential. 
Currently we only accept [did:polygonid](#did:polygonid) issuers and holders.

For example.

- Issuer: `did:polygonid:polygon:main:2qCU58EJgrELSJT6EzT27Rw9DhvwamAdbMLpePztYq`.
- Holder: `did:polygonid:polygon:main:2q544HUegzeRpwr3V2qu9eMwgrAmF5x4E1NCPzbQc4`.

Currently your users will be able to create an identity using the PolygonID wallet, which can be downloaded [here](https://play.google.com/store/apps/details?id=com.polygonid.wallet&hl=en_US). 

BLOOCK Identity will soon expand support for more [identity wallets](#what-is-a-wallet?).

### What is a wallet?
A digital wallet is an application or software designed to protect and manage identities or holders. A wallet allows you to interact with the Issuer when we want to obtain or acquire our credentials and interact with the Verifier to share and verify our proofs contained in our credentials.

A wallet is controlled by an identity and therefore must have its own DID. That is why, in most of these wallets when we install the application the identity it's created. That identity will control the wallet. For example, the PolygonID wallet creates an identity like this: `did:polygonid:polygon:main:2q544HUegzeRpwr3V2qu9eMwgrAmF5x4E1NCPzbQc4`.

Each wallet must follow a communication protocol in order to interact with the Issuer and the Verifier. For example, PolygonID wallet follows the [DIDComm protocol](#dIDComm-messaging).

### The Verifier
The Verifier is the entity responsible for receiving and processing verifiable credentials. 

The verification process consists of the evaluation of whether a Verifiable Credential is an authentic and current statement of the Issuer. This includes checking that: the credential conforms to the specification; the proof method is satisfied; and, if present, the status check succeeds.

The Verifier is responsible for issuing a request to the Holder. This request contains the queries that the Holder must fulfill to be verified. [Here](#verification-queries) to learn more about queries.
The request of the Verifier is designed and encapsulated into a QR code to be shown to the Holder. The Holder scans the QR code with its [Wallet](#what-is-a-wallet?) to prompt the proof generation.

The verification process doesn’t involve any interaction between the Verifier and the Issuer of the requested credential. As part of the Query, the Verifier includes the identifiers of the trusted issuers.

At the end of the process, the verifier gets a cryptographic proof that the Holder satisfies or not the query.

This is the process that a verifier would perform:
1. Generates the Query request and display it for the Holder to be checked.
2. Initiate a waiting process to obtain verification.
3. Validate the cryptographic proof generated by the Holder and allow access, or otherwise, if it is invalidated, block access.

At BLOOCK Identity we offer you a verification model, but it is important that depending on your business model, you can customize it as much as you want. We perform a polling and expiration verification. Once the Verifier creates the Query request to the Holder, it starts what we call a verification process, which consists of simply polling a function that returns whether the request has been verified correctly or not (it returns a boolean). This polling process also has a timeout that you can configure. In addition, the verifications have a default expiration of 60 minutes, meaning that the Query request has an expiration of 60 minutes. If a user is already validated but the 60 minutes time expires, he/she will have to be validated again, this expiration period is also customizable.

The Verifier must choose which type of proof to verify (you can only verify one type of proof).
- [Atomic Query Signature V2](#signature-proof): cryptographically verify the proof of signature of the credential.
- [Atomic Query Sparse Merkle Tree V2](#sparse-merkle-tree-proof-(SMTP)): cryptographically verify the sparse merkle tree proof of the credential.

### Verification queries
BLOOCK Identity works with Zero-knowledge proof [(learn more about it here)](#zero-knowledge-proof). For this, we work with [Query language](https://devs.polygonid.com/docs/verifier/verification-library/zk-query-language/) specification, to provide a simple way for developers to design customized authentication requirements for someone's credentials.

As long as the user holds a credential of a specific type, the Verifier can design a query based on 6 operators, for example:

1. Must have an employment status of "active" to access sensitive company data - `equals` (operator 1).
2. Must have joined the company before 2020-01-01 to be eligible for the company's pension plan - `less-than` (operator 2).
3. Must have a monthly salary greater than $2000 to qualify for a company car lease - `greater-than` (operator 3).
4. Must be a manager or an IT specialist at BLOOCK to access the server room - `ìn` (operator 4).
5. Must not be a resident of a country in the list of restricted travel destinations to attend company events abroad - `not-in` (operator 5).
6. Must not be a resident of the state where the company's rival firm is located to be considered for a promotion - `not-equal` (operator 6).

> Currently you can only verify a single attribute of a Verifiable Credential. This means that your Query request will only be able to verify for example that the BLOOCK employee is born before 2020-01-01. If, for example, you want to verify another attribute you will have to generate a new Query request. 

### Zero-knowledge proof
_In cryptography, a zero-knowledge proof or zero-knowledge protocol is a method by which one party (the prover) can prove to another party (the verifier) that they know a value x, without conveying any information apart from the fact that they know the value x._ ([Source](https://en.wikipedia.org/wiki/Zero-knowledge_proof))

In other words, zero-knowledge proofs allow us to prove something specific without revealing any extra information.

BLOOCK Identity works with this type of proofs technology, so the security and privacy of your users' credentials is very high, because when they verify their credentials, the data itself is never shared.

### DIDComm messaging
BLOOCK Identity uses the DIDComm messaging protocol for communication between agents and wallets. The purpose of [DIDComm Messaging](https://identity.foundation/didcomm-messaging/spec/) is to provide a secure, private communication methodology built atop the decentralized design of [DIDs](https://www.w3.org/TR/did-core/). We use this protocol with the [Iden3comm](https://iden3-communication.io/). 



## Understand the flow
Let's describe how an end-to-end flow works to see how all the terms described above relate to each other in BLOOCK Identity.

### Create Baby JubJub key
In order to create an identity in BLOOCK Identity I will first need to create or have a Baby JubJub (BJJ) key. This key will be very important to have it saved because it will be used to control our Issuer.

I have two options to get this key.
1. You can create a BJJ key with our managed key product ([BLOOCK Keys product](go_to_keys_documentation)), your key will be identified by a UUID. This identifier will be enough to control your Issuer.
`Example: 6f36448d-49f3-4b0e-aa72-6e55863302e8`
2. If you have created a BJJ type key locally, i.e. you are aware of its private key, then you can use it to control your Issuer.
`Example: bf5e13dd8d9f784aee781b4de7836caa3499168514553eaa3d892911ad3c345j`

### Create the Issuer
Once we have our key available, we will create the Issuer.  
Before creating the Issuer we should think about how often we want the status of our Issuer to be transacted. [Here](#issuer-intervals) you can see what intervals we have available. If you need information to make this decision you can contact us. For this example, let's imagine that I choose a 60-minute interval.

Once we have our Issuer we can see its identity represented with its [DID](#decentralized-identifiers-(DIDs)) (decentralized identifier). This is unique and totally public, this DID is directly related to the key you have created previously.
`Example: did:polygonid:polygon:main:2qCU58EJgrELSJT6EzT27Rw9DhvwamAdbMLpePztYq`

### Create the schema
Next, we must think about what type of credentials we want to issue. For example, we want to issue a card that identifies BLOOCK employees. In order to create the schema I have to follow these steps.
1. I must first think about the name of the schema type, in this case for example it would be BloockEmployee.
2. I must define what attributes my credential will have, for example, I will put an employee number, name and date of birth.

Once this is defined, I will be able to create my schema. Notice that all we are doing is defining the attributes that our credentials will have.

[The schemas](#schemas) are uploaded to IPFS, in order to identify the schemas we use their IPFS identifier.
`Example: QmadTvnNKvj2fBDgen35uAp1TfP9pSPVCNeDWw4fitqqne`

### Create the credential
To create a credential, we will need two very important things.
1. I need the schema identifier that it will reference, which will therefore mark which attribute structure it will have. In my case it will be my employee number, name and date of birth.
2. I will need the BJJ key created for that Issuer, because when we create a credential let's remember that in order to be verifiable we need to be able to sign it and get a proof of authenticity.
3. You should know who is going to be the Holder of this credential or rather which is the user who is going to receive this credential. This Holder must have created his own identity at the same time. For example, in the case of our employee for whom we are going to issue this credential, the following DID identifies him/her: `did:polygonid:polygon:main:2q544HUegzeRpwr3V2qu9eMwgrAmF5x4E1NCPzbQc4`.
4. We will also be able to add additional metadata such as expiration date, version number, etc...

Once the credential is created we will obtain a UUID identifier.
`Example: 0e3199ac-8147-4c7a-938b-d33f9107dace`

The most important thing is that this credential is already a [Verifiable Credential (VC)](#the-verifiable-credential-(VC)) because it already includes a signature proof, and therefore, this credential would already be valid to be verified by any verifier.

But BLOOCK Identity's product offers a second test, related to integrity in blockchain.
The [Sparse Merkle Tree proof](#sparse-merkle-tree-proof-(SMTP)) is a proof that will be available depending on the [interval time](#issuer-intervals) you have chosen and is related to the Issuer's state. 
As I have previously chosen a 60 minutes interval, it means that I will have my SMTP proof available after ~60 minutes.

### Credential offering
The credential offering process refers to the transfer of the Verifiable Credential (VC) to the assigned user or Holder. 
It requires two agents (Issuer and Holder) and a [wallet or software](#what-is-a-wallet-?) where the credential will be stored. 
At the Holder level, this is done by scanning a QR code generated by the Issuer from the Holder's wallet. 
At the protocol level this communication is highly secure thanks to the [DIDComm protocol](#dIDComm-messaging) used and the authentication and identity proofs mechanisms.

Therefore, to execute the offering.
1. The Issuer generates a request QR code.
2. The Holder autonomously scans this QR code with his credential management application or wallet.
3. The Holder authenticates and verifies his identity to the Issuer, who, once approved, sends him the Verifiable Credential.

### Verify the credential
TODO!

### Revoke the credential
TODO!
