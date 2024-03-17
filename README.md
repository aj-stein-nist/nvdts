# nvdts

This code base is a proof-of-concept implementing one interpretation of the [SCITT architecture](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-06.html#name-terminology) and supporting IETF Internet Drafts and RFCs below to simulate [the CVE ecosystem, its process](https://www.cve.org/About/Process), and the [National Vulnerability Database](https://nvd.nist.gov/) in particular.

## Concepts and actors

Hopefully, you have read [the above](#nvdts), but this is a proof-of-concept architecture and implementation that will need to simulate multiple actors representing different organizations. SCITT is fun to use and experiment with, but (near) real-world experiments require the concept of these multiple actors and organizations. At this time, the actors below are part of this simulation and concept.

With the SCITT architecture, there are several important roles for different people, organizations, and their systems to simulate with this representation of the National Vulnerability Database.

1. Issuers
1. Transparency Service Operators
1. Verifier Operators
1. Auditors

Let's address each one of them one by one.

### SCITT Issuers are CVE CNAs

### SCITT Transparency Service Owners are CVE Program and NVD Staff

### SCITT Verifier Owners are community and industry service owners

### SCITT Auditors are System Auditors using NVD TS data

### Simulated Process

The simulation of CVE identifier requests, registration, and disclosure will transpose the [CVE reporting process](https://www.cve.org/About/Process) and NVD analysis into the high-level process workflow of SCITT transparency services, described below using the [current SCITT architecture terminology](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-06.html#name-terminology).

1. A security researcher determines there is vulnerability about software (an Artifact) they want to report, so they prepare a Statement about that Artifact to register with the CVE CNA (an Issuer).
1. They submit the Statement about the the Artifact through the CNA service, which is an Issuer, signs it to make a Signed Statement in preparation for [registration](https://www.ietf.org/archive/id/draft-ietf-scitt-architecture-06.html#name-registration-policies)
1. The CVE Transparency Service receives the Signed Statement and verifies the Signed Statement's signature.
1. After signature verification, the CVE Transparency Service validates the headers and payload content of the Signed Statement. 
1. The service analyzes the Signed Statement after verification and validation to confirm the payload of the Signed Statements meets the CVE Transparency Service's current registration policy.
1. After registration policy conformance and prior steps are successfully completed, the Signed Statement is registered to the Append-only Log of the CVE Transparency Service.
1. The CVE Transparency Service returns a Receipt to the Issuer's automation system that polls the Transparency Service after the registration is complete and the Transparent Statement is now available and accessible on the Append-Only Log.
1. Auditors can operate software to "replay" the CVE Transparency Service to confirm the proper operation of the service, ordering, and consistency of the Append-only Log's integrity.
1. Operators of downstream services that enrich, analyze, and mix-in other data sources with the CVE data operate SCITT verifiers to analyze selected Transparent Statements of interest to their use case. They may use Subjects to filter the CVE Transparency Service and retrieve Transparent Statements about specific Artifacts, for example, specific versions of one or more software releases.

## Architecture

The current SCITT architecture and [SCRAPI specification](https://datatracker.ietf.org/doc/html/draft-ietf-scitt-scrapi-01) drafts presuppose a HTTP-based API for registration of Signed Statements and retrieval of Transparent Statements. This system will simulate the creation of a Append-only Log and this HTTP API by generating the backing content of the Append-only Log and a limited subset of API responses at build time, much like static site generators for different websites. An HTTP service can host the resulting content, be it [GitHub Pages](https://pages.github.com/) or [AWS S3](https://aws.amazon.com/s3/).

## Acknowledgements

I thank members of the IETF SCITT WG, the [scitt.io community], and all colleagues from NIST and the larger open-source community. You know who you are.

This [architecture](#architecture) was inspired by Orie Steele's design with [endor](https://or13.github.io/endor/), so he deserves special praise after consulting me on reviving this approach.