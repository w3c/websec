DRAFT for team discussion, 14 October, 2015, wseltzer@w3.org 

# W3C Security Strategy #

Securing the Web is a multi-layered challenge. To secure the Web
experience of end-users: its confidentiality, integrity, and
authentication; we need to provide tools for end-users, for
application developers, and for platform security. Moreover, the
security of Web applications depends on underlying protocols, on
browser and server software, hence we need to enlist the cooperation
of participants throughout the ecosystem. A joint approach, can help
re-establish trust in the platform as a place for commerce and
communication, addressing concerns of an increasing number of Web
users. We must address these challenges now because individual and
enterprise users are demanding greater security and privacy; if we do
not respond constructively, we risk losing trust in the platform, and
losing users to other forms of interaction.

# Goals

Through our security and privacy efforts, W3C aims to establish
justified trust in the Web platform. We aim to provide the components
to uesrs and developers to assure the integrity, authenticity, and
confidentiality of interactions on the Web. We must also assure that
W3C Recommendations are high-quality and do not introduce new security
vulnerabilities as they add new capabilities to the platform. 

We enlist the support of the Web community in reaching these goals,
through a strategy that can be described in three layers:

- Web user security

- Web application security

- Web platform security

We also note that some security challenges are outside our ability to
affect directly: operating environment and lower-level protocol flaws,
poorly coded implementations, and human error cannot be specified
away. Working to assure that we introduce no additionl security flaws,
but rather tools for security improvement, we can cooperate to raise
the Web platform.

# 1. Web User Security #

At the most user-facing level, we are working to secure the login and
authentication experience and support secure communication channels. 

* Web Cryptography API

[WebCrypto](http://www.w3.org/2012/webcrypto/) provides a first step
toward enabling secure authentication and communication from the
browser. The
[Web Cryptography API](http://www.w3.org/TR/WebCryptoAPI/) spec,
currently in Candidate Recommendation and implemented across major
browsers, provides standard APIs to cryptographic functions such as
encryption, decryption, signing, hashing, and verification. WebCrypto
allows a web developer to build in their application a reliable
security model protecting the user (such as authentication or secure
communication between the browser and the server).


* Authentication

Building on the multi-factor authentication work of the
FIDO Alliance, [Secure Authentication] will aim to standardize
multi-factor authentication for the Web, using the combination of
"something you have" with "something you know," so that hacking a
password database is no longer sufficient to hijack user
accounts. [Hardware-based Security] aims to improve the levels of
assurance to which users and application providers are able to protect
their online accounts and communications, by making hardware security services available to the Web.

* HTTPS for Communications and Data Security

The [Privileged Contexts](http://www.w3.org/TR/powerful-features/)
draft recommends that powerful features of the Web platform, including
application code with access to sensitive or private data, be
delivered only in secure contexts, over authenticated and confidential
channels that guarantee data integrity. As the draft indicates,
"delivering code securely cannot ensure that an application will
always meet a user's security and privacy requirements, but it is a
necessary precondition."


# 2. Web Application Security #

Users' security also depends on Web application authors' ability to
ensure that their applications are delivered as intended, free from
spoofing, injection, and
eavesdropping. [WebAppSec](http://www.w3.org/2011/webappsec/) is
addressing this challenge from several angles.

* Content Security Policy

[Content Security Policy](http://www.w3.org/TR/CSP/) provides a policy
language by which application developers can declare a security policy
for a web resource. The goal of this specification is to reduce attack
surface by specifying overall rules for what content may or may not
do, thus preventing violation of security assumptions by attackers who
are able to partially manipulate that content, for example by script
injection or cross-site request forgery. An application delivered over
a secure channel with CSP enabled can assure that users receive it as
it was intended to be executed. New tools, such as Subresource
Integrity enable the secure incorporation of aditional elements into
the application.


* HTTPS support

Several specifications help Web application developers HTTPS-enable
their Web Apps, including the
[Upgrade Insecure Requests](http://www.w3.org/TR/upgrade-insecure-requests/)
and [Mixed Content](http://www.w3.org/TR/mixed-content/)
drafts. These, along with work such as HSTS and HPKP, help to ease the
HTTPS transition for server operators, and as the proportion of HTTPS
traffic grows, set user expectations that Web traffic should be
secure, integrity-protected, and authenticated.

* Visibility and Sandboxing

Upcoming in WebAppSec, [IronFrame] proposes to eliminate clickjacking
by assuring element visibility at the graphics rendering level. A
developer deploying IronFrame can assure that users clicking their
site's "pay" button aren't being tricked into transferring their bank
balances to an imposter instead. Prompted by the
[Digital Marketing Workshop](https://www.w3.org/2015/digital-marketing-workshop/agenda.html),
we may see proposals for new sandboxing capabilities, to permit the
trustworthy mash-up of active content from multiple sources.

#3. Web Platform Security #

Finally, we need to make the Web Platform a place users can expect and
demand security from all their interactions. That entails upgrading
the baseline security and privacy of Web interactions -- supporting
the HTTPS roll-out; standardizing permission requests; sharing best
practices; and assuring that all specifications include security and
privacy considerations.

* HTTPS transition

The WebAppSec work described above not only helps to secure the
experience of the applications that use HTTPS, but also set user
expectations about the platform. As more providers deliver their Web
applications via HTTPS, users and their user-agents can exercise a
preference for secure applications.

* Security and Privacy Considerations.

The [TAG](https://tag.w3.org/), WebAppSec, and
[Privacy Interest Group](http://www.w3.org/Privacy/) are developing a
[Privacy and Security Self-Review Questionnaire](https://w3ctag.github.io/security-questionnaire/)
to help groups assess the privacy and security implications of their
specifications. To make such self-review a routine part of groups'
progress along the Recommendation-track, we would like to require that
every spec include a "Security and Privacy Considerations" section --
and ensure that WGs have access to expert advice to review and address
these considerations effectively. We can do that via Process changes
or guidance to and from the Director at transition reviews. Since
effective security review of specifications requires participation of
subject-matter experts (Working Group participants) and security
experts, we believe that a strong signal to stakeholders in the work
will help to spur that participation: a signal from the Director that
drafts will not advance to Candidate Recommendation without explicit
Security and Privacy Considerations need not depend on a change to the
Process, but such a change may help to bring it to Members' attention.

* Internal Liaisons

An increasing number of W3C groups are recognizing that their specs
will require security design in order to succeed. These include Web
Payments, Web and Automotive, Web of Things, and Web Platform. To help
them design security and privacy into their architecture, where it can
be most effective, we propose to work toward a team of community
liaisons who can work between PING / WebSec and the subject-specific
WGs, becoming internal experts on the subject matter and its security
and privacy implications. 


# Focus for 2016 #

* Improved authentication: Secure Authentication and Hardware-Based
  Security
* Web Application Security: keep specs moving forward
* Improved reviews: Chair training, team and community expert advice;
  require Security and Privacy Considerations
* Internal liaison with security requirements around W3C: Web
  Payments, Web and Automotive, Web of Things, Web Platform
