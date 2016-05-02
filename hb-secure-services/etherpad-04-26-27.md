Notes and Outputs from the W3C Hardware-based Secure Services Workshop, London  - 26th and 27th of April 2016.


IRC minutes: Live minutes were captured on W3C's IRC, #hb-secure-services

Day 1, 26th April 2016: https://www.w3.org/2016/04/26-hb-secure-services-minutes.html
Day 2, 27th April 2016: https://www.w3.org/2016/04/27-hb-secure-services-minutes.html


# Use Case Discussions


Paul Waller, CESG. "Secure by default".  
* replacing large numbers of passwords, software-based crypto for authentication
* risk management of devices fleet and services,
* for government as an enterprise this includes internal services such as web services & email, but also authenticating to a device e.g. disk encryption & VPN
* for citizen services online
Challenges: how to diffentiate service among devices, while presenting the right level of detail to users; how to accumulate confidence (e.g., among multiple methods)
* trusted input and output (how do I know what I see on screen was what provider sent)
* end-to-end secure messaging to an unmanaged device?
"I need to send a message to a user on a previously unseen device" how to bootstrap trust? known device ID, trusted display? 
* attestation (TCG, characterizing entire device state; here, perhaps, attestation about device security level) This could just be key attestation, e.g. what sort of credential store is protecting the key used to sign this response?  Doing this securely requires a device certificate, which must be inserted duing production
*solution must be general across a range of different devices, capabilities
* hardware key storage


Is there a half-way step? so we don't need to solve everything at once.
Understand the work that already exists, making the business case for integration. 
Hardware-backed security for identity and government services. 


Less about increasing security, than improving usability for what currently exists




Identity inside the browser (in order to avoid external service )
(to be detailed)


Philip Hoyer, HID Global
[this is a technology trend, not a use case]
TEEs in >450M devices
Contactless protocols maturing
HW sec primitives becoming cheaper, e.g. ECC
HW IDs increasing in number: drivers license, patient IDs, eID, 
endpoint architectures multiplying


Important:- Dichotomy:  Authentication & Identity 
                  - consent recording, signing, voting


usability improvements, getting to user-acceptable speeds for secure transaction
continuous/frictionless authentication *and* explicit user consent (e.g. signing, voting, payment)


Aurelien Couvert, Gemalto
thoughts from Gemalto's secure element API. 
cross-platform secure element (SE) API . 
needs access control to the secrets in the SE. 
globalplaform.github.io/??
http://globalplatform.github.io/WebApis-for-SE/doc/


transport level api similar to sim alliance omapi
se manager-reader-session-channel
access control toolbox. 
web security model: permissions, same origin policy
se security model. PIN, secure messaging (mutual authN), GlobalPlatform access control 
GP Access Control: whitelist, which apps can access what in the SE
Boxes: Web/ [public API] / privileged apps. e.g. AuthN, Signature, Payment, Reload / [restricted API] / SE

pallette: trusted services, SE built-ins, GP Access Control, domain binding. 

Typical Access control scenario: Access managed hardware
reuse of existing security building blocks, creative combination


Joerg Heuer and Peter Hofman, Deutsche Telekom
we've shown a mobile wallet, something that keeps state outside the browser, communicates through the browser.
T-Systems, systems integration. public ticketing. Why are we currently using barcodes or QR codes? 
virtual car key in user wallet, provisioned for car rental. 


Use cases: car key, ticketing, payments (securing online payments as "card-present"); access control; hw-backed authentication
We know how to virtualize the hardware, don't know how to virtualize for the Web


Sebastien Bahloul, Morpho
sharing experience about identity, use case. 
eID, good practices re level of assurance
* states' motivation: public safety, public services (digital 50x cheaper), capabilities 
* level of assurance (defined by the lowest security level of id proofing, authentication factor, id & authentication lifecycle)


Features: update profile of card; reload credits; renew certificate; deliver identity attributes. 


Browsers won't accept unscoped "APDU API". Maybe they will. Chrome for example accepts unscopeed "USB" API provided the user grants permission.
how do we communicate between high-level, low-level API. 


propose: transaction confirmation API first. including authentication, transaction confirmation, signature
"what you see is what you confirm."
requires trusted output, TEE






Technical Discussion and Requirements  for designing a solution




(we might start high level and then refine)


* About the solution
consider also implementability and economic sustainability of the deployments.
be agnostic in terms of implementation as a good implementation strategy today is to deploy in software first and use hardware
 APDU will never be available to web developers
giving user "trust context" about the information passed (range from medium to high security) - we may need to be more objective to start with - identifying the make and model of the credential store, for example, plus a statemetn of any certifications held.
The solution must be able to run on any type of hardware (NFC reader, smart card, TEE, TPM)
The solution can get benefit of all communication layers available in the device where the browser runs (NFC, BLE, USB, ISO, ....)
The solution must have an access control and request user consent to access the hardware crypto device (to allow who should access the secure element services)
The solution must no send unscoped bearer tokens around
need to mix/bridge web security model and secure element security model (and web service provider security/risk management model)
The secure services might have a root trusted issuer (pre-existing identity delivered by a trusted service provider, CA for certificate management)
The solution may be able to include a user consent (improving the context and recognizing the consent aspects, à la FIDO)
(Note that the association between user and credential might be out of scope)
The solution must follow the SOP (and may build means to avoid being strict about it)
The solution must support multiple users crypto and identity details.
the solution must be able to block repeated request (to avoid attack by repeating)
the solution may be end to end (aka, user agent being a tunnel to pass the data)


* About the usability and user perspective
Insure security with usabilitibity, 
user must be able to choose to whom (and as whom) he/she is recognised
user interest/choice must be heard (either he/she cares or does not care to give information away) --> right to reconsider choice
The solution must be usable on any browser
A common interface/way to interact to choose the service is important
The solution may have a detailed security qualification of the storage (private information)


The solution must be usable for people with disability (either with a replacement mean, or an special care for context description)






*Web service perspective
Web service providers should be able to enforce policies for certain types of transactions (e.g. login with sw-credentials, but transaction signing with HW token)


Privileged javascript as a proposal. 
Trusted javascript for trusted operations
Rate limitation for the number of subsequent requests to the crypto token


Vocabulary aspects :
* Make a clear difference between an unmanaged device and untrusted device
* Make clear identity and credentials are two different things


Open question : 
    what happens if the service provided by the hardware technology disappears ? Error management/border case has to be managed
    Does W3C have to define user interaction ?
    What is the information that can be brought from the hardware token to the web layer
    


---
Adrian Castillo. 
capabilities: read from card
services: secure channel between token and server, need the keys from card issuer
runs on IE and FF, Windows; MacOS Safari


Sebastien Bahloul. 
API looks the same with the presence or absence of hardware features; it's up to the service provider to determine how to handle varying levels of assurance. 




Some things we can do : 
    
* List what other standards do
and their gaps
* Define a new protocol, with end-to-end authentication between hardware and server
would that get ecosystem support
* Beware of monocultures


* Catalog what Apps can do that browsers can't
* secure credential storage, keychains, and protections 
(issuance, renewal, revocation) (use)
* key attestation
* environment attestation 
* trusted UI 
* transaction confirmation service
* biometry
* a strong application security management (access control, digital signature, permissions, ...)
* discoverability / reminder of the tokens used
* app curation


* Define which types of hardware tokens (besides smart cards) shall be supported on which transport channels on desktop and mobile platforms (e.g. USB authentication/signature tokens, smart wearables via BLE/mobile,...)


---
Use cases: 
    
    * User confirming a transaction (request for several markets and scenario)
Government online benefit payment systems (4B in payments); e.g. citizen management of change of address, WYSIWYC; 
Banking, adding a new external account. Adding beneficiaries. Transferring money (between a user's accounts; from one user to another)
Confirm a trade
Legal binding : digital signature on contract. Message signature. Note : Legal binding needs possession and knowledge (like in banking cards at the ATM)
personal, or business. (delegation, agency): signing as a principal or as an agent of the company 


Access to e-government services, health care
trusted proof of claim. 


consequence of that use case deployment : 
    --> need to have a qualification of the 'material' used for the transaction confirmation , like a key attestation - knowing (the security of) where the key ended up


    * credential management  (request for several markets and scenario)
Reputation management based on token owned by the user : comments on the web, on social media...
All the use cases mentionned in the transaction confirmation
Secure messaging : allowing an end to end encryption (Whatsapp recent choice)
    related technology : web crypto API 
    reinforce WebCrypto use cases with higher security    https://www.w3.org/TR/webcrypto-usecases/
      
Use case: A tangible hardware thing carrying individual or company identity token used for services and authentication that is of moderate security, e.g. for time management and cafeteria


--
# APIs
* Secure Credential Storage (elaborated below)
* Transaction Confirmation API 



# Transaction Confirmation API - Champion: Sebastien
flipchart image: https://github.com/w3c/websec/blob/gh-pages/transaction_confirmation.jpg

JavaScript API
Goal: to give some assurance to a remote entity that a transaction is confirmed. Confirm that what was sent was communicated to the user, and that what was displayed to the user is what was confirmed.  Confirmation should include a signature and also some information about the secure environment (which vendor, is it hardware, is there tamper protection, is there any certification- with clarity of both display and input as these may have seperate security "levels") - this will help the remote entity understand how confident they can be in the response.
May depend on key attestation; trusted UI. 
[assuming the component has already been provisioned]


enum CVM { "presence", "active" , "none"?};
[ref FIDO, test of user presence or active authentication]
[added "none" to cater for passive authentication use-cases, where the service provider only needs device authentication]


interface SubtleHWCrypto { 
  Promise<any> checkPresence(BufferSource dts);
  Promise<any> confirm(DOMString context, CVM mode, String url); 
  Promise<any> sign(DOMString context, BufferSource dts);
};


Signing both the context and the data.
Relies upon X509 certificates 


Acronyms and Definitions


SP/RP - Service Provider/Relying party - e.g. a bank
Context: A message to the user that is human readable
SCS - Secure Credential Store
KMS - Key Management Selection
KML - Key Managment List
NRA - Non-repudiation Acknowledgment (M=Message)
TEE - Trusted Execution Environment
OS - Operating System
MW - Middleware
UVM: User Verification Method


Use Cases for this API


* Non-confidential use case
* Confidential use case


IBAN to IBAN transfer (transaction from foreign bank to UK customer) - out of the zone of the local banking system, very difficult to resolve later / traceability issues
* both ends have total clarity of the transaction


Usage Flow


1. user consults an HTML page provided by SP (service provider)
2. the browser checks SOP/CORS JS call to a browser API 
3. the browser gathers information with respect to the UI, execution environment, potential certification, OS quality
3.bis : [Trusted Environment (not browser controlled)] discovery of certificate the user chooses credential or keys to be used for signing 
4. the user signs data and context (presented in human understandable way)
5. the browser collects signature and transfers to SP




Scheme flow
parties : user/SP or RP/ Browser / Transaction confirmation component (TUI TEE, OS, middleware, code running in the browser), 


https://www.websequencediagrams.com/?lz=dGl0bGUgVHJhbnNhY3Rpb24gY29uZmlybWF0aW9uCgpwYXJ0aWNpcGFudCBFbmQtdXNlciBhcyBFVQAODVNlcnZpY2UgUHJvdmlkAB0GU1AAMQ1Ccm93ADYHQlIASw1UcnVzdGVkICBVSSAoVEUsIE9TIG9yIE1XKSBhcyBUVUkAXA9jdXJlIFN0b3JhZ2UAdQVlciAoZVNFLCBTSU0sIE5GQy9CTEUgU0UgLi4uAD8FU0NTCgpFVS0-U1A6IFJlcXVlc3Qgc2Vuc2l0aXZlIG9wZXIAgWoGU1AtPkJSOiBEZWxpdmVyIHRoZSBIVE1ML0pTIHBhZ2UKQlIAGwZKUyBjb21wdXQAgiEHYWx0IE5STSBvbmx5IChub24gcmVwdWRpAIJCBSkKICAgIEJSLT5UVUk6IE4AEA4AgmUNIHIAgRcHd2l0aAAlBVIAHwtNZXNzYWdlIChOUk0pCmVsc2UAcAUrIERUUwBlESArIGJpbmFyeSBzaWduZWQgZGF0YQA1ViBhbmQgRGF0YSBUbyBTaWduIChEVFMAgRsHRFRTAIIQB3RyYW5zcGFyZW50IAABCwCEZg0Agh0PAIUVBQAUEwCCGgYAXxRuZAoKVFVJPC0-U0NTOiBLZXkgbWF0ZXJpYWwgbG9va3VwAIMJJVRVSS0-RVU6IFByZXMAgSwFaGUgY29udGV4dCwAhBMFawBODHNlbGUAhjoGYW5kIHJldHJpZXZlAIQ7BQCGLgV2ZXJpZmljAIZQBiAgICBFVQCEBwdVABoFYWxpZACECAYoVVYpICsAhBQRYWNrbm9sZXdkZ2VtZW50IChOUkEpICsAgQEFAHMKKEtNAIJvCACDZDUANYFBAIQ9MACEKgUAg2coAIRMBQCINwhOUk0AhlQFYXR1cmUAh1wFU0NTAIdbBwCKAAcAhnEITlJNAIJUQAA_PACBKhZEVFMAgTYKAIhpBnRoZSBzYW0AhVUGdXNlZCB0bwCIOAUAPgkAgUoZRFRTAIc0OgB9ICh3aGljaACGbAU_AIpGBgBqHgCHfAcAi0UGAIJ9D2VsAIY7BXMAij8FIGFuZC9vciBEVFMpICsgVFVJIEF0dGVzAItQBiArIFNDUyBhAAgKAIt6BVNQAINXCgCIDwZtYmluZWQgAIpwEHJlc3VsdAo&s=vs2010




Note : Transaction confirmation component is in charge of taking care of non repudation, presenting the context. Non-repudiation (can also be used for transaction confirmation and consent recording)
Note : Context message is a text only, localised, presented to the user by the Transaction confirmation module. 
Note : NRA is ? Non-repudiation Acknowledgment (M=Message)
Note : KMS is Key Management Selection - key selected by user
Note: KML is Key Managment List - acceptable keys from SP point of view
Note : SCS: Secure Credential Store
Note : attestations are associated with Transaction Confirmation Module and SCS




Assumptions / Dependencies


* Browser: JavaScript, HTML, CSS
* Underlying Trusted Execution Environment / capability
* Reliability
* Human user OR machine-to-machine?
* The Trusted UI integration in browser should not be mandatory in the service usage
* We can think usage flow from the POV: "we have nice new capabilities on mobile phones, let's bring it to the web". 
* Or we can think the same usage flow from: "I have a web application written in javascript and I want to have secured consent recording/authentication 
   and I want to access certain hardware capabilities". 
* Everything which has to be signed is firstly signed by the SP and the hardware secure device would have to first verify it before letting the user signing it
* The signature is operated by the hardware token, and has a direct link with the Transaction Confirmation Component
* Dependency on X.509 certs => Yes
* Dependency to Permission API (WebAppSec WG).  https://www.w3.org/TR/permissions/ to ask for permission to use hardware capabilities (mention the type of operation as well, not only access required but access to sign?)
* GlobalPlatform doesn't mind additional APIs as long as it does not break the protection profile (UI) only needed if addtional information 
  is needed by the trusted application from the TEE, not if web application wants something from the secure application. 


Errors and Exceptions


* User blocks / denies access
* Invalid / untrusted domain
* Invalid keys
* Certificate expiry
* OCSP / CRL error (what is this flow?)
* Timestamp error
* latency, network errors


Security Considerations


* The "dancing pigs" problem around user confirmation / presence
* Availability and Integrity requirement
* Vulnerabilities in underlying OS
* Vulnerabilities in browser
* How the browser collects and stores (hopefully not cached in software) information about the underlying platform / execution environment
* Signing mode Trusted UI should show the choice of certificates/keys - ideally user should 
*Patches/updates - how do I know the 'trusted' remote component is up to date? / version number as well as type, should be recorded. May not be necessary to be validated?
* Need to have a consistency of context security descriptionand secuirty error management for accessibility reasons




Threats / Attacks


* Extraction of user data by unauthorised site / person
* Cross-site scripting attacks (breach of SOP)
* Man in the browser attacks
  * including through underlying OS vulnerabilities
  * including malicious browser extensions
* Repudiation attacks
* Time abuse attacks / NTP / local
* Replay attacks
* Abuse of accessibility services to leak / modify information or to display different information between the interfaces
* abusing signature sent back to the RP (bearer token as mentionned by rigo) (scope the bearer tokens used e.g. to date, origin, transactionnumber)
* Attacker fakes the entire system / user interaction process




* Phishing / social engineering
* Semantic attacks e.g. mixing fonts / making something look like the authentic SP (the RoyBan problem)


Privacy Considerations
* Browser is not a confidential environment
* Privacy-preserving attestation of environment
* Confidentiality requirements? 
* authentication and exposure of user credentials or uniqueIDs etc should only happen after user interaction (like geolocation) 
    [abuse also by trusted parties in the form of dark patterns]
* recording consent as a feature


User Considerations


* Recording consent
* Readibility of security context - user display / understanding
* indication - e.g. TEE display hardware indicator / user stored image
* User education
* Terms and conditions / display
* Accessibility: some equipment is not designed for accessibility / out-of-band mechanisms


General Concerns


* In esignature law - Display component needs to be certified by government? Possible in a browser [Germany]? Rigo: may not be a concern


Where is this flow currently used? How is it done? (source of example use cases, refinements to the model)
* e.g. transfer from account A to account B, DTS is "account number"+context


Work in progress about verifyable attributes: https://www.websequencediagrams.com/?lz=dGl0bGUgVmVyaWZpYWJsZSBhdHRyaWJ1dGVzCgpwYXJ0aWNpcGFudCBFbmQtdXNlciBhcyBFVQAODVNlcnZpY2UgUHJvdmlkAB0GU1AAMQ1Ccm93ADYHQlIASw1UcnVzdGVkICBVSSAoVEUsIE9TIG9yIE1XKSBhcyBUVUkAXA9jdXJlIFN0b3JhZ2UAdQVlciAoZVNFLCBTSU0sIE5GQy9CTEUgU0UgLi4uAD8FU0NTCgpFVS0-U1A6IFJlcXVlc3QgdmVyAIFfEVNQLT5CUjogRGVsaXZlciB0aGUgSFRNTC9KUyBwYWdlIApCUgAcBkpTIGNvbXB1dGF0aW9uCgATBVRVSQBVCnRvIHJldHJpZXYAgkYMIHdpdGggU1AgcHVibGljIGtleSBhbmQgbm9uY2UKVFVJPC0-U0NTOiBBACkKYXZhaWxhYmlsaXR5ClRVSS0-RVU6IFByZXNlbnQAgR4FcgBWHmZvciBhIHRhcmdldCBTUCAoVVJMIG9yIGRvbWFpbiBuYW1lKQCCGgUAgTwFVXNlciB2YWxpZACBVgUgKFVWKQCBMQZlAIN4CWNrbm93bGVkZ2VtZW50AIEPBgCBMgUAglUIAIFnC2QAgkYGeSwgc2lnbmF0dXJlAIFuBQCBdw5lbmNyeXAAgkcFU0NTAIJFBwCESAcANAVlZACCJAUAIQdlZACFGwwAghAFQlIACCkgKyBTQ1MgYXR0ZXMAgzoHQlIAhBgGAGsIdGhlIGRhdGEgYmFjayB0bwCEBgVTUAo&s=vs2010


----
# Secure Credential Storage and Management
(Credential=cryptographic keys)


Introduction text  
Goal: To provide for the secure storage and management (issuance, renewal, revocation) of keys for, e.g. identification, authorisation, signature
Scope limitation : we will not manage X509 or any other certificate straucture, but only focus on keys.
two possible use cases : (1) a credential is provisioned by one RP and used by the same RP, (2) a credential is provisionned by a RP and used by other authorised. 
Decision : Lets start with one case 1 and work on use case 2 on the basis of (1)


Use cases : to be detailed, having in mind use cases where user is in control, and use cases where the RP is in control. 


Technical assumption and requirements


Portability should to be considered  (aka, using any key in a token inserted in any browser)


Credential sharing : organization may create credentials to be used by other parties [question: do we require use of a derived credential rather than the original? possibly advantageous from a comprise scenario]
There have to have an access control to control third parties, but still fitting with SOP. A possible solution is to add some metadata (aka, authorised domains to use the credential [question: what are good ways to scale such whitelisting?])


Revocation : a credential may be revoked by the issuer (invalidated) and a authorised SP may also be removed (its access to the credential can be revoked - by whom, the user or the credential-issuer?)


Renewal : TBD
ACTION : Rigo will come back with an explanation of a potential technical solution for sharing credentials among parties. 




Functionality : 
    We want key to be able to be permanent (persistent) 
    We want key to be protected from hardware and software attacks
    Do we want this key non-extractable by default? We may keep both both possibilities, with wrapping capabilities
    Do we want only to use crypto in the hardware token? We don't want to restrict the possibility of extraction. 
    Can we migrate keys? (wrapped) - use cases?
    Do we want to extract keys (in plain text)? - use cases?
    Portability of keys - is the key bound to the device or module? (Bound to a URI origin) - installed into a physically removable device or a non-removable device? Can you attest to the difference? e.g. some information/knowledge about that device helps for the SP etc. - e.g. signed make, model, version number
    Selectable [processing] sources - e.g. hashing could be done in the token or in software, for example for performance / efficiency needs
    Note : the speed of operation may be a discriminative point to have the browser being involved in crypto operations.
    
    We want the web developer to be able to choose the level of security of the hardware token used.
    In the future we may want have the possibility for the user to choose the token he wants to use. 
    We want the UA to be able to handle multiple keys origin [key identity?] clash, 
    We want the UA to be able to retrieve keys from a specific origin


    Suggested MVP : create key, private stays inside, public can be exported,s key is used to sign/cipher within the hardware crypto token [with preference to /dev/urandom*]
    Key Destruction - SP initiated (security risk of it becoming a kill switch!) and user initiated (e.g. a device factory reset / transfer ownership of device)
    
    Different types of keys, some may be associated with user validation/control - needs use cases to explain this properly. Don't want to make this unusable due to [prompting]
    - management aspects to this too (related methods)
    - triggering self-management UI etc. [security issues?]
    There should not be a requriement that requires the security module must make security assets held by other components of the device. i.e. it cannot be expected that the TEE must have access to PIN valdiation assets that are held by the Rich OS. 
    open question : do we want the user to be associated with the creation of a key ? if yes, it may be in the form of a user verification (pincode, fingerprint) (also generation of entropy for randomness[*]). The use case could be the user is looking for free spacing. 


Note: the W3C Key Discovery Note can be reused: https://www.w3.org/TR/webcrypto-key-discovery/


[Interoperability expectation especially if moved around between devices...]
[bootstrapping?]


Usage Flow (Full lifecycle of keys needs to be further described)


Secure Storage


First use case : RP wants to create a key to enable secure cloud storage. Initial context is that the user is using a browser on the website of the upbox service.


1. User wants to store a photograph she is uploading to the upbox photo service.
2. Browser calls JavaScript API to initiate Key generation in secure hardware
3. Ciphering operation in secure hardware
4. Encrypted Photograph is uploaded to upbox.


Second use case : User decides to download the image from the upbox cloud service. Context is the same as above.


Security goal for this service - prevent leakage of photo to other devices whilst storing it in the cloud. [Note to reader: we need the other use cases for multiple devices / shared services]


1. User initiates the download of the encrypted picture from upbox.
1.1 Key discovery via JavaScript call to keydiscovery function - from secure hardware.
2. The JavaScript call to the decryption function is called within the browser. 
3. Decryption operation.
4. Plaintext image is displayed within the browser in the context of the upbox website.
[or unwrapped key in key storage]


Not mentioned here - unwrapping/key manipulation within the secure hardware or within the browser context, dependent on various factors (such as, having one secret key created per document, protected by the master key of the service)


Information: possible keys: user, upbox, individual key for photo




https://www.websequencediagrams.com/?lz=dGl0bGUgUlAgd2FudHMgdG8gY3JlYXRlIGEga2V5IHRvIGVuYWJsZSBzZWN1cmUgY2xvdWQgc3RvcmFnZQoKcGFydGljaXBhbnQgRW5kLXVzZXIgYXMgRVUADg1SZWx5aW5nIHBhcnR5IGFzIFJQAC4NQnJvdwAzB0JSAEgNVHJ1c3RlZCAgVUkgKFRFLCBPUyBvciBNVykgYXMgVFVJAHYNUwCBHwZTAIEZBiAoZVNFLCBTSU0sIE5GQy9CTEUgU0UgLi4uADgFU0NTCgoKb3B0IFVwbG9hZACBHAVob3RvCiAgICBFVS0-UlA6IFVzZXIgdG8AgW4FZSBlbmNyeXB0ZWQgcmVzb3VyY2Ugb24gdGhlIHNlcnZpY2UANwVSUC0-QlI6IERlbGl2ZXIgSFRNTC9KUwBTBUJSLT5TQ1M6AIFrCWNhbGxzIEphdmFTY3JpcHQgQVBJIHRvIGluaXRpYXRlIEtleSBnZW5lcmF0aW9uIGluAIMECGhhcmR3YXIAbgZCUjwAUgdDaXBoZXJpbmcgb3AAFCEAgV8GRQCBTglQaG90b2dyYXBoIGlzIHUAghQFZWQgdG8gdXBib3guCmVuZACCLwZEb3duAIIqDXMAgiYSAIE8CHMAgh4FZAArByBvZgCCLgUAgkMKcGljdHVyZSBmcm9tAGEIAII8DQAyCEpTIGFuZACCfAtkYXRhAIFxD0tleSBkaXNjb3ZlcnkAgmYOc2VuAINiBQAtE1NDUwCDLwZTAB0HYmFjawCBMQZlAGEMAIETBkJSAINcBmRhdGEgaXMgZGlzcGxheWVkAIIbBQ&s=vs2010


Third use case: Accessing an eGovernment service and altering information


1. User receives email from town administration to update information about children for subsidies
2. User directs his browser to https://town.gov.ee and clicks on the link to the changing service
3. town.gov.ee sends a page with JavaScript that requests access to the hardware with the Estonian citizencard
4. The page requests to activate the citizencard from the users
5. The user accepts the request and puts the citizencard near the NFC reader
6. town.gov.ee sends a challenge
7. Browser signs challenge with the user's private key  from eID Citizencard<-- new API is used here !
8. town.gov.ee sends the page with the form to change the information to the user
9. The user fills out the form and clicks "submit authenticated"
10. The browser hashes and signs the form and sends it to town.gov.ee
11. town.gov.ee verifies the form with the user's public key from eID Citizencard
12. town.gov.ee updates the database for children subsidies




Security Considerations


* Loss / theft of device [means that user can never access content if tied to the key] - key extraction / backup use case


Privacy Considerations






Exceptions and Errors


* card/token not present / removed




Usability for Web Developers


* We want web developers to be able to understand the subtle security options of the API.
* Education!
    
Usability for End Users


* Reduce opportunities for social engineering / fraud.


Accessibility






Dependencies and References
* Not duplicating FIDO's authentication work. 
* FIDO is doing authentication without identification. Hardware credentials most often are tied to some identity management scheme. So the big difference 
   on what we try to achieve here is to use the hardware credential INCLUDING identification and not only device authentication. 
* WebCrypto API: https://www.w3.org/TR/WebCryptoAPI/
* Credential Management, WebAppSec
* Unclear whether X.509 credentials will have to be used and what else is ready or good or an option. We should start with normal key management. 
* A challenge in Web Crypto: different formats used in different places (OS native functionality needs a bridge to work interoperably across platforms). Relying on native OS may introduce difficulty in interoperability
* Ahana points to https://d0.awsstatic.com/whitepapers/KMS-Cryptographic-Details.pdf 


Suggestion is to transport the hardware capabilities in metadata once the user agrees to expose them. The web developer will be able 
to create algorithms of which method to use and when to fail with an error message. This is related to the W3C Note on Key Discovery (no 
implementation of key discovery so far)


Rationale


Problem: browser password stores are weakly protected in some browsers/OSes; localstorage may not be secure;
browser auto-complete may supply information meant to be kept secure
Suggestion from David: Expose the problem space first to have a narrowly scoped target work that may convince browsers




How do Same Origin Policy and Shared Credentials work together? 
*  per-origin enrollment? a la FIDO, Android fingerprint sensor, TPMs with attestation keys. 
* Rigo s idea is to use a session encryption like in OTR to have the origin added to the general certificate. Will refine the idea with Sebastien




About Implementations Considerations


Aurélien : 
    in a secure element, keys are handled into applet, there is a need to have a standard way to create keys and manage it...for example, choosing PKCS11 style of talking to a secure element.
    
    Peter :
Code needed in multiple places, including from browser to TEE and SE. That's a challenge for industry. 
Virginie: possible open source projects to work with: https://www.linaro.org/
Open TEE project https://github.com/Open-TEE/project


https://www.w3.org/community/hb-secure-services/



