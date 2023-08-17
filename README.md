# `did:knox` Method Specification
## Introduction
Identity is often proven today via either physical ownership of credentials (e.g., a driver’s license or passport) or online via a list of usernames and passwords on centralized services over the internet. These solutions lack privacy, with both methods exposing more data than is necessary to parties in a transaction. For example, age verification might require the showing of a driver’s license, which includes additional personal information like date of birth, address, and name. In reality, the only thing that must be proven is a verifiable way of knowing the answer to the binary question “Is this user over 21?”. While showing whole credentials may be acceptable to a person who may not remember, this exposure is not a best practice over the internet. With traditional identity systems, users store usernames and passwords on external centralized servers that are easy to forget and get reused in dozens of systems such that a single security breach exposes access to the rest of the victim’s associated systems.
Knox aims to ensure sensitive data stays in the user’s secure storage, interacting (Ex authenticating, signing, verifying, etc) with cryptographic proofs of identity data instead of usernames/passwords along with manual PII via W3C Decentralized Identifiers (DID) and Verifiable Credentials (VC).  Knox in particular focuses on problems with current payment systems that leave consumers feeling they've lost control of their privacy, while still allowing financial compliance when required.  Some systems require PII to be sent to a server on every transaction, some require sharing of transaction data on public ledgers which can be analyzed and correlated to certain users.

## Design Goals
In order to increase adoption and bring traditional identity systems to this Self Sovereign Identity (SSI) model that leverages W3C DIDs and VCs, Knox attempts to achieve this bridging with currently familar industry standards operated at large enterprises such as financial institutions/banks. Knox will layer on top of existing identity systems and data sources to migrate the data in to DID/VCs in user wallets, which then can be used for transactions. Minimal data should be sent only when required for financial compliance (ex AML/CFT), and such logic can be implemented in wallets depending on the transaction type.  As institutions adopt digital assets/currency platforms which are Public Key Infrastructure(PKI) based, DIDs become the natural solution to enable the optimal balance of privacy and compliance, and Knox uses public keys as part of the DID for simpler translation.  As scalability and cost are blockers to adoption, the did:knox registry avoids being locked to a blockchain, avoiding expensive consensus algorithms and is designed to be hosted by a trusted operator- ex Bank consortium.  While blockchains make sense in De-Fi, in regulated assets/money there is less decentralization required when it comes to DID Registry responsibilities transacting through trusted institutions.  The `did:knox` method is somewhat similar to a combination of `did:key` and `did:web` except that instead of relying on HTTP servers for storage, it can rely on distributed database technologies design for higher scale and reliability.

## Knox DID Identifier Syntax
- **DID Method Name**: knox<br>
Additional institutional identifiers can be considered if required to be on separate registries- Ex `did:knox:institutionAId`
The signature system support is `Ed25519Signature2020` by default but can be configured to use other systems. Ex `Secp256k1` based.

## Example

```
- did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy
```
## Knox DID Document

The basic structure of a DID Document in Knox is as follows:
```json
{
  "@context":[
    "https://www.w3.org/ns/did/v1",
    "https://w3id.org/security/suites/ed25519-2020/v1"
  ],
  "id":"did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy",
  "authentication":[
    {
      "id":"did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy#z23fgBTfnsAF8PnYjJJPBLLRB5NJtNaWrUPPf6P4BdmucM",
      "type":"Ed25519VerificationKey2020",
      "controller":"did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy",
      "publicKeyMultibase":"z23fgBTfnsAF8PnYjJJPBLLRB5NJtNaWrUPPf6P4BdmucM"
    }
  ],
  "capabilityInvocation":[
    {
      "id":"did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy#z23wU6rXC6VeMjGLwbNr3EHytcabDa5nmaSucYLVLk4L3E",
      "type":"Ed25519VerificationKey2020",
      "controller":"did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy",
      "publicKeyMultibase":"z23wU6rXC6VeMjGLwbNr3EHytcabDa5nmaSucYLVLk4L3E"
    }
  ],
  "capabilityDelegation":[
    {
      "id":"did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy#zr5tzEJNgepzEXxpk9PRJK1pKRYrFsNXTgfMMpx6Qmpgr",
      "type":"Ed25519VerificationKey2020",
      "controller":"did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy",
      "publicKeyMultibase":"zr5tzEJNgepzEXxpk9PRJK1pKRYrFsNXTgfMMpx6Qmpgr"
    }
  ],
  "assertionMethod":[
    {
      "id":"did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy#z23PE75QbknqhbwURgvvo8etkg7KKNXgx6B3qeUvPtrkgn",
      "type":"Ed25519VerificationKey2020",
      "controller":"did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy",
      "publicKeyMultibase":"z23PE75QbknqhbwURgvvo8etkg7KKNXgx6B3qeUvPtrkgn"
    }
  ],
  "service":[
    {
      "id":"did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy#issuer-registry",
      "type":"IssuerRegistry",
      "serviceEndpoint":"http://bar.example.com/{issuerId}"
    }
  ]
}
```
This JSON object is a Decentralized Identifier (DID) Document, conforming to the W3C's DID Specification. Each property has the following meanings:
- `@context`: This property specifies the standard or specification to which this DID Document conforms. In this case, it shows that the W3C's DID v1 standard and the ed25519 cryptographic suite are used.
- `id`: This property is a unique identifier for the DID Document, used to reference this Document. Here, the ID is `did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy`.
- `authentication`: This property includes an array of IDs for verification methods that can be used for authentication using this DID.
- `capabilityInvocation`: This property includes an array of IDs for verification methods that can be used to invoke capabilities.
- `capabilityDelegation`: This property includes an array of IDs for verification methods that can be used to delegate capabilities.
- `verificationMethod`: This property contains an array of methods that the DID owner can use to prove their identity. The objects within this array contain the following properties:
- `assertionMethod`: This property includes an array of IDs for verification methods that can be used to make claims or signatures using this DID.

For detailed information on the DID Document, you can refer to the W3C's DID Specification document.
## CRUD Operation
### Create/Register
The `did:knox` method supports the creation of Decentralized Identifiers (DIDs). The generated DID and associated DID Document are stored within the Knox application service via `create` API which allows for future cryptographic interaction with the DID subject.

### Read
The `did:knox` method supports two functionalities: resolver and dereferencer.
- `resolve`: The resolver's resolve function permits holders to access their DID Documents held in the verifiable data registry via their Knox DID. This function embodies the read operation on the decentralized identity infrastructure, aligning with the guidelines set forth in the W3C DID Specification. This ensures secure and standardized access to individual DID Documents, further cementing the decentralized nature of identity management facilitated by the Knox DID method.
- `derefererence`: The dereference functionality provided by Knox allows for retrieval of specific property values from the Knox DID Document through a DID URL. For instance, a specific value such as the service endpoint from the service attribute within a holder's DID Document can be obtained.
### Dereference Example
```json
{
   "dereferencingMetadata":{
      "contentType":"application/ld+json"
   },
   "contentStream":{
     "id": "did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy#issuer-registry",
     "type": "IssuerRegistry",
     "serviceEndpoint": "https://bar.example.com/{issuerId}"
   },
   "contentMetadata":{}
}
```
### Update
A holder can update their DID Document located in the verifiable data registry through the Knox application service via `update` API.
### Delete/Revoke
A holder has the ability to delete their DID Document from the verifiable data registry through the Knox application service via `revoke` API.
## Privacy / Security Consideration
The wallet service using the `did:knox` method should implement industry best practices for security such as storing private data and keys inside the wallet enclave, network transport security (ex TLS v1.3, mTLS, etc), not logging sensitive data, data leaving the wallet only when required, and ensuring the data does not get exposed to other local apps in the case mobile/device apps. 

The DID Document should not have any PII and the DID service configured should be careful to not correlate the subject easily to certain accounts. To proactively avoid correlation and use of compromised keys, keys should be rotated periodically and the DID Document `verificationMethod` can support additional new keys while old ones are removed.  

Issuer DIDs should be check against the Trusted Issuer Registry, and VCs revocation status should be check via `CredentialStatusList`, provided with `did:knox` registry.  

For additional privacy compliance such as GDPR, DID Documents can be deleted from the registry to comply with requirements such as "Right To Erasure".

## Reference
[Decentralized Identifier Resolution (DID Resolution) v0.3](https://www.w3.org/TR/did-core/)<br>
[DID Specification Registries](https://www.w3.org/TR/did-spec-registries/)<br>
[Verifiable Credentials Data Model v1.1](https://www.w3.org/TR/vc-data-model/)<br>
[Verifiable Credentail Implementation Guideline](https://w3c.github.io/vc-imp-guide/#web-authentication)<br>
[DID Identifier Resolution](https://w3c-ccg.github.io/did-resolution/)<br>
