# Knox DID Specification
Knox-did-specification which is conforming W3C-DID-Specification
## Motivation



## Goal

## Knox DID Identifier Syntax
- **DID Method Name**: Knox<br>


## Example

```
- did:knox:z2BgV8eWjwoQLKJeZqYqKmNozD9PqRTiiaBLUSVEXQRJjy
```
## Knox DID Document

The basic structure of a DID document in Knox is as follows:
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
The Knox DID libraries enables the creation of Decentralized Identifiers (DIDs). The generated DID and associated DID Document are stored within the Knox application which allows for the verification of the integrity of the DID Document during data access or updates.

### Read
The Knox DID method supports two functionalities: resolver and dereferencer.
- `resolve`: The resolver's resolve function permits holders to access their DID Documents held in the private data registry via their Knox DID. This function embodies the read operation on the decentralized identity infrastructure, aligning with the guidelines set forth in the W3C DID Specification. This ensures secure and standardized access to individual DID Documents, further cementing the decentralized nature of identity management facilitated by the Knox DID method.
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
A holder can update their DID Document located in the personal data registry through the Knox application.
### Delete

## Privacy / Security Consideration

## Reference
[Decentralized Identifier Resolution (DID Resolution) v0.3](https://www.w3.org/TR/did-core/)<br>
[DID Specification Registries](https://www.w3.org/TR/did-spec-registries/)<br>
[Verifiable Credentials Data Model v1.1](https://www.w3.org/TR/vc-data-model/)<br>
[Verifiable Credentail Implementation Guideline](https://w3c.github.io/vc-imp-guide/#web-authentication)<br>
[DID Identifier Resolution](https://w3c-ccg.github.io/did-resolution/)<br>
