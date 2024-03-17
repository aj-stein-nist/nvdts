# nvdts

This code base is a proof-of-concept implementing one interpretation of the [SCITT architecture](https://datatracker.ietf.org/doc/draft-ietf-scitt-architecture/) and supporting IETF Internet Drafts and RFCs below to simulate [the CVE ecosystem, its process](https://www.cve.org/About/Process), and the [National Vulnerability Database](https://nvd.nist.gov/) in particular.

## Concepts and actors

Hopefully, you have read [the above](#nvdts), but this is a proof-of-concept architecture and implementation that will need to simulate multiple actors representing different organizations. SCITT is fun to use and experiment with, but (near) real-world experiments require the concept of these multiple actors and organizations. At this time, the actors below are part of this simulation and concept.

### SCITT Issuers are NVD CNAs

### SCITT Transparency Service Owners are NVD Staff

### SCITT Verifier Owners are community and industry service owners

### SCITT Auditors are System Auditors using NVD TS data