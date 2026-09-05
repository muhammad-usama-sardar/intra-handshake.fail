<div align="center">

# Intra-handshake.fail (CVE-2026-33697): </br> High-severity (CVSS 7.5) CVE in Attested TLS

[![License](https://img.shields.io/badge/license-Apache--2.0-blue)](LICENSE)

<p align="center">
  <img src="images/logo.png" width="400"><br>
</p>

# [Paper](https://www.researchgate.net/publication/408219182_Intra-handshakefail_CVE-2026-33697_High-severity_CVE_in_Attested_TLS) and  [Internet-Draft](https://datatracker.ietf.org/doc/draft-intra-handshake-fail/) </br>

</div>

## Overview

This repo contains the artifacts for formal specification and analysis of the candidate binding mechanisms for binding in intra-handshake attestation for standardization for attested TLS protocols:
<!---
TODO: Present as table: Binder # and Meaning
--->

<div align="center">

| No. | Binding mechanism | Used in | Artifacts |
|---|---|---|---|
| 1. | Client’s TLS nonce | [Meta's AI](https://ai.meta.com/static-resource/private-processing-technical-whitepaper) | [binder1](./binder1/) |
| 2. | Client’s attestation nonce | - | [binder2](./binder2/) |
| 3. | Early exporter | - | [binder3](./binder3/) |
| 4. | Server’s public key | - | [binder4](./binder4/) |
| 5. | Combination of #2 and #3 | - | [binder5](./binder5/) |
| 6. | Combination of #2 and #4 | [Edgeless Systems Contrast](https://github.com/CCC-Attestation/meetings/blob/main/materials/MarkusRudy.contrast-atls-ccc-attestation.pdf) </br> [Cocos AI](https://www.ultraviolet.rs/products/cocos-ai/) </br> [CCC Attestation SIG](https://github.com/CCC-Attestation)'s adopted project [intra-handshake attestation](https://github.com/ccc-attestation/attested-tls-poc)| [binder6](./binder6/) |
| 7. | Combination of #2, #3, and #4 | [draft-fossati-tls-attestation-06](https://www.ietf.org/archive/id/draft-fossati-tls-attestation-06.html) | [binder7](./binder7/) |
</div>

> [!CAUTION]
> We provide a formal proof of insecurity of all the above candidate binding mechanisms of intra-handshake attestation using the state-of-the-art tool [ProVerif](https://ieeexplore.ieee.org/document/9833653) and propose a mitigation for the discovered security vulnerabilities. Our study reveals that it may not be possible to achieve strong application-traffic (level 3) binding using intra-handshake attestation alone. This can be exploited for relay attacks, where an attacker makes a client accept an evidence from a different machine. So the client cannot be sure that it connects to its desired server.

We *responsibly* disclosed the vulnerability in intra-handshake attestation -- as noted in [security advisory issued](https://github.com/ultravioletrs/cocos/security/advisories/GHSA-vfgg-mvxx-mgg7) -- to the vendors, which resulted in CVE ([CVE-2026-33697](https://www.cve.org/CVERecord?id=CVE-2026-33697)) of CVSS 7.5.

## Detailed vulnerability disclosure timeline

<div align="center">

| Event | Date |
|---|---|
| Our initial responsible disclosure to vendor | 07 Oct, 2025 |
| Acknowledgement by vendor | 14 Dec, 2025 |
| Information to the [IETF](https://mailarchive.ietf.org/arch/msg/rats/6gbqx0XY8WYrH3Mx4vO8n2-uKgY/) | 11 Jan, 2026 |
| [Public announcement](https://web.archive.org/web/20260227160554/https://www.ultraviolet.rs/blog/tee-tls-privacy/) by vendor | 27 Feb, 2026 |
| Cocos AI published [security advisory](https://github.com/ultravioletrs/cocos/security/advisories/GHSA-vfgg-mvxx-mgg7)  [**Severity = HIGH (CVSS 7.8)**] | 23 March, 2026 |
| CVE ([CVE-2026-33697](https://www.cve.org/CVERecord?id=CVE-2026-33697)) published  [**Severity = HIGH (CVSS 7.5)**] | 26 March, 2026 |
| [CCC implementation](https://github.com/ccc-attestation/attested-tls-poc) declared [vulnerable to relay attacks](https://github.com/CCC-Attestation/attested-tls-poc/pull/58) | 17 July, 2026 |
| Vulnerable [CCC implementation repo](https://github.com/ccc-attestation/attested-tls-poc) archived | 22 July, 2026 |
| Vulnerable draft [draft-fossati-tls-attestation](https://datatracker.ietf.org/doc/draft-fossati-tls-attestation/10/) withdrawn by authors |  23 July, 2026 |
| Edgeless Systems published [security advisory](https://github.com/edgelesssys/contrast/security/advisories/GHSA-hjgc-jc5v-fw7h)  [**Severity = HIGH (CVSS 7.4)**] | 29 July, 2026 |

</div>

### Comparison with other vulnerabilities in confidential computing literature

Severity is based on [NIST metrics](https://nvd.nist.gov/vuln-metrics/cvss).

<div align="center">

| Vulnerability | CVE | CVSS | [Severity](https://nvd.nist.gov/vuln-metrics/cvss) |
|---|---|---|---|
| [wiretap.fail](https://wiretap.fail/files/wiretap.pdf) | No CVE ([Intel](https://www.intel.com/content/www/us/en/security-center/announcement/intel-security-announcement-2025-10-28-001.html) and [AMD](https://www.amd.com/en/resources/product-security/bulletin/amd-sb-3040.html) announcements) | - | None |
| [TEE.fail](https://tee.fail/files/paper.pdf) | No CVE | - | None |
| [TDXdown](https://dl.acm.org/doi/10.1145/3658644.3690230) | [Intel](https://www.intel.com/content/www/us/en/security-center/announcement/intel-security-announcement-2024-10-08-001.html) | 2.5 | Low |
| [Staleus](https://xca-attacks.github.io/staleus/staleus_usenix26.pdf) | [CVE-2025-54509](https://nvd.nist.gov/vuln/detail/CVE-2025-54509) | 4.0 | Medium |
| [BreakFAST](https://xca-attacks.github.io/breakfast/breakfast_oakland26.pdf) | [CVE-2025-61972](https://nvd.nist.gov/vuln/detail/CVE-2025-6197)| 4.2 | Medium |
| [BadRAM](https://badram.eu/badram.pdf)| [AMD](https://www.amd.com/en/resources/product-security/bulletin/amd-sb-3015.html)| 5.3 | Medium |
| [BreakFAST](https://xca-attacks.github.io/breakfast/breakfast_oakland26.pdf) | [CVE-2025-61971](https://nvd.nist.gov/vuln/detail/CVE-2025-61971)| 5.9 | Medium |
| [Fabricked](https://xca-attacks.github.io/fabricked/fabricked_usenix26.pdf) | [CVE-2025-54510](https://nvd.nist.gov/vuln/detail/cve-2025-54510)| 5.9 | Medium |
| Intra-handshake.fail (this work) | [CVE-2026-33697](https://www.cve.org/CVERecord?id=CVE-2026-33697) | 7.5 | High |

</div>

The comparison of the above with CVSS 7.5 for intra-handshake.fail indicates that attested TLS is not mature yet compared to the rest of the confidential computing stack, and is currently one of the weakest links in the ecosystem. We are investigating further and we are confident there are more high-severity vulnerabilities in intra-handshake attestation which are yet to be discovered.

<p align="center">
  <img src="images/relayAttacks.gif" width="400"><br>
  <sub><i>Figure 1: Simplified relay attack for mechanism #1.</i></sub>
</p>

## Affected Implementations
- [Meta's AI](https://ai.meta.com/static-resource/private-processing-technical-whitepaper): [CVE-2026-33697](https://www.cve.org/CVERecord?id=CVE-2026-33697) [**Severity = HIGH (CVSS 7.5)**] 
- [Cocos AI](https://github.com/ultravioletrs/cocos): [security advisory](https://github.com/ultravioletrs/cocos/security/advisories/GHSA-vfgg-mvxx-mgg7)  [**Severity = HIGH (CVSS 7.8)**] and [CVE-2026-33697](https://www.cve.org/CVERecord?id=CVE-2026-33697) [**Severity = HIGH (CVSS 7.5)**] 
- [Edgeless Systems Contrast](https://github.com/edgelesssys/contrast): [security advisory](https://github.com/edgelesssys/contrast/security/advisories/GHSA-hjgc-jc5v-fw7h)  [**Severity = HIGH (CVSS 7.4)**]
- [CCC Attestation SIG](https://github.com/CCC-Attestation)'s adopted project [intra-handshake attestation](https://github.com/ccc-attestation/attested-tls-poc): declared [vulnerable to relay attacks](https://github.com/CCC-Attestation/attested-tls-poc/pull/58) and archived

## Binding Levels
1. DH shared secret (`gxy`) used as shared secret between client and server
2. Handshake traffic key (`htsc`) used for encryption of handshake messages
3. Application traffic key (`atsc`) used for encryption of application data

## Correlation Goals
We consider TLS Server as RATS Attester, which is typical in confidential computing.

1. Correlation of Evidence to a DH Shared Secret (G1)
2. Correlation of Evidence to Client’s Handshake Traffic Key (G2)
3. Correlation of Evidence to Client’s Application Traffic Key (G3)

## Main results

- All analyzed binding mechanisms and the corresponding implementations of intra-handshake attestation are vulnerable to relay attacks.
- Early exporter helps achieve level 1 binding.
- Our proposed mechanism helps achieve level 2 binding.
- It may not be possible to achieve level 3 in intra-handshake attestation alone without additional assumptions.

<div align="center">

| Property                   	        | Mechanism #1,2,4,6 | Mechanism #3,5,7 | Proposed mechanism |
| :--                		              | :--    | :--   | :--   |
| G1 : Correlation of Evidence to `gxy` | ❌     | ✅    | ✅    |
| G2 : Correlation of Evidence to `kch` | ❌     | ❌    | ✅    |
| G3 : Correlation of Evidence to `kc`  | ❌     | ❌    | ❌    |

</div>

### Expected results

<div align="center">

| No. | Binding mechanism | Artifacts | Expected results |
|---|---|---|---|
| 1. | Client’s TLS nonce | [binder1](./binder1/) | [binder1](./binder1/log.txt) |
| 2. | Client’s attestation nonce | [binder2](./binder2/) | [binder2](./binder2/log.txt) |
| 3. | Early exporter | [binder3](./binder3/) | [binder3](./binder3/log.txt) |
| 4. | Server’s public key | [binder4](./binder4/) | [binder4](./binder4/log.txt) |
| 5. | Combination of #2 and #3 | [binder5](./binder5/) | [binder5](./binder5/log.txt) |
| 6. | Combination of #2 and #4 | [binder6](./binder6/) | [binder6](./binder6/log.txt) |
| 7. | Combination of #2, #3, and #4 | [binder7](./binder7/) | [binder7](./binder7/log.txt) |
| 8. | Proposed | [proposal](./proposal/) | [proposal](./proposal/log.txt) |

</div>

### Implications of Research for IETF SEAT WG
- We believe post-handshake attestation alone, such as [draft-fossati-seat-expat](https://datatracker.ietf.org/doc/draft-fossati-seat-expat/), can achieve level 3 binding.
- The research suggests that recent hybrid proposals (combination of intra-handshake attestation and post-handshake attestation) [draft-fossati-seat-early-attestation](https://datatracker.ietf.org/doc/draft-fossati-seat-early-attestation/04/) and [draft-ritz-seat-facts](https://datatracker.ietf.org/doc/draft-ritz-seat-facts/00/) may add unnecessary complexity of intra-handshake attestation without adding any security benefit compared to post-handshake attestation alone, such as [draft-fossati-seat-expat](https://datatracker.ietf.org/doc/draft-fossati-seat-expat/).


### Implications of Research for IETF TLS WG
- Remote attestation *within* the handshake is very dangerous, since to our knowledge, it is one of the highest scored vulnerabilities in confidential computing literature (see [this](https://github.com/muhammad-usama-sardar/intra-handshake.fail#comparison-with-other-vulnerabilities-in-confidential-computing-literature)).

> [!CAUTION]
> We very strongly recommend the developers and maintainers of intra-handshake attestation to urgently move to post-handshake attestation.
 
<!---
#❓
--->

## Artifacts author
Muhammad Usama Sardar (contact: muhammad_usama.sardar at tu-dresden.de)

## Paper authors
Muhammad Usama Sardar, Viacheslav Dubeyko, and Jean-Marie Jacquet

## Pre-print
Preprint is available [here](https://www.researchgate.net/publication/408219182_Intra-handshakefail_CVE-2026-33697_High-severity_CVE_in_Attested_TLS).

## Scientific Publication
The work is accepted for publication at ESORICS and should be cited as follows: 

> Muhammad Usama Sardar, Viacheslav Dubeyko, and Jean-Marie Jacquet. 2026.
Intra-handshake.fail (CVE-2026-33697): High-severity CVE in Attested TLS.
In 31st European Symposium on Research in Computer Security (ESORICS) 2026,
September 14-18, 2026, Rome, Italy. LNCS,
20 pages.

BibTeX:
```
@inproceedings{Sardar2026IntraFail,
author = {Sardar, Muhammad Usama and Dubeyko, Viacheslav and Jacquet, Jean-Marie},
booktitle = {Proceedings of the 31st European Symposium on Research in Computer Security (ESORICS) 2026},
publisher = {LNCS},
title = {{Intra-handshake.fail (CVE-2026-33697): High-severity CVE in Attested TLS}},
year = {2026}
}
```

For Internet-Drafts:
```
  Intra-handshake.fail:
    title: "Intra-handshake.fail (CVE-2026-33697): High-severity CVE in Attested TLS"
    date: September 2026,
    target: https://www.researchgate.net/publication/408219182_Intra-handshakefail_CVE-2026-33697_High-severity_CVE_in_Attested_TLS
    author:
      - ins: M. U. Sardar
      - ins: V. Dubeyko
      - ins: J-M. Jacquet
```

and then use as ``{{Intra-handshake.fail}}``

For citing this repo:
```
  Intra-handshake.fail-repo:
    title: "Intra-handshake.fail (CVE-2026-33697): High-severity CVE in Attested TLS"
    date: June 2026,
    target: https://github.com/muhammad-usama-sardar/intra-handshake.fail
    author:
      - ins: M. U. Sardar
      - ins: V. Dubeyko
      - ins: J-M. Jacquet
```

and then use as ``{{Intra-handshake.fail-repo}}``

## Acknowledgments
We gratefully acknowledge the following for insightful discussions on this work:

- Eric Rescorla
- Juho Forsén
- Markus Rudy
- Mariam Moustafa
- Bruno Blanchet
- Steve Kremer
- Tjaden Hess
- Martin Thomson
- Yuning Jiang
- Pavel Nikonorov
- Casey Wilson
- Danko Miladinovic
- Songbo Bu
- John Preuß Mattsson
- Werner Staub
- Nathanael Ritz

We also gratefully acknowledge the following who gave feedback on [previous state-of-the-art](https://github.com/CCC-Attestation/formal-spec-id-crisis) that we utilize as the basis:

- Tuomas Aura
- Ionut Mihalcea
- Thomas Fossati
- Hannes Tschofenig
- Yaron Sheffer
- Laurence Lundblade
- Giridhar Mandyam
- Christopher Patton
- Jonathan Hoyland
- Richard Barnes

Several others at the IETF, IRTF, and CCC have contributed by providing feedback.

We sincerely thank Karthikeyan Bhargavan, Bruno Blanchet, and Nadim Kobeissi for the foundational formal model of draft 20 of TLS 1.3 in their [work](https://ieeexplore.ieee.org/document/7958594).

## Tool 
We use state-of-the-art symbolic security analysis tool [ProVerif](https://ieeexplore.ieee.org/document/9833653) for the specification of the protocols. 
### Installing ProVerif
Install the latest version (2.05 at the moment) of ProVerif: see https://bblanche.gitlabpages.inria.fr/proverif/ for details.
See Section 1.4 of [manual](https://bblanche.gitlabpages.inria.fr/proverif/manual.pdf) for installation options:
- via OPAM: Section 1.4.1
- from sources: Section 1.4.2 or simply try the [script](https://github.com/CCC-Attestation/formal-spec-TEE/blob/main/installProVerif.sh) by replacing 2.04 by 2.05
- from binaries: Section 1.4.3 

## Modeling

The formal model uses the [fixed version of diversion attacks in intra-handshake attestation](https://github.com/CCC-Attestation/formal-spec-id-crisis/tree/main/TLS-a/fix) from our previous work as the starting point to focus on relay attacks in intra-handshake attestation in this work.
The rationale is that we consider it more useful to show the added value of this contribution to the community by using the [fixed version of diversion attacks in intra-handshake attestation](https://github.com/CCC-Attestation/formal-spec-id-crisis/tree/main/TLS-a/fix) as the baseline, rather than showing the same diversion attacks from [ID-Crisis paper](https://dl.acm.org/doi/10.1145/3779208.3785387), and the discovered CVE (CVE-2026-33697) -- which the previous analysis could not find -- practically demonstrates the added value.
This modeling choice makes it clear that even with the diversion attacks fixed, high-severity relay attacks would still remain in intra-handshake attestation.

Note: Similar to the [fixed version of diversion attacks in intra-handshake attestation](https://github.com/CCC-Attestation/formal-spec-id-crisis/tree/main/TLS-a/fix) from our previous work, we model non-PSK-based handshake.
From [ID-Crisis paper](https://dl.acm.org/doi/10.1145/3779208.3785387):

> For modeling TLS 1.3, we consider handshakes based on Diffie-Hellman over either finite fields or elliptic curves, represented as (EC)DHE. This is because we are unaware of any publicly available specification or implementation of attested TLS with PSK-based handshakes.

While it would be nice to model PSK-based handshake, the rationale is that the correlation properties studied in this work do not necessarily require it.

> [!NOTE]
> The artifacts consider the case of server authentication only, as client authentication is optional in TLS 1.3. No claims are made about other configurations.

## Artifacts organization

> [!TIP]
> The artifacts are quite flexible for modification and testing of different intra-handshake attestation binding mechanisms by simply changing single `rdata` parameter in the `Client` and `Server` processes. Folder `aggregate` contains all [analyzed](https://github.com/muhammad-usama-sardar/intra-handshake.fail#overview) and proposed binding mechanisms to select via comment and uncomment. Other folders contain one specific binding mechanism.

<details>
<summary>Click to expand folder details</summary>

- Folders `binder1` till `binder7` contain code for [binding mechanism](https://github.com/muhammad-usama-sardar/intra-handshake.fail#overview) #1 till #7, respectively.
- Folder `proposal` contains code for our proposed binding mechanism for mitigation.
- Folder `aggregate` contains code for all analyzed and proposed binding mechanisms to select via uncomment.

</details>

The name of files within each folder are the same. So the following [commands](https://github.com/muhammad-usama-sardar/intra-handshake.fail#running-automatic-proofs) can be used to run any of those.

```text
intra-handshake.fail/
│
├── README.md                        # README file
│
├── aggregate/                       # Uncomment the desired binding mechanism
│     ├── tls-lib-simple.pvl         # ProVerif library file for correlation properties
│     ├── other-props.pvl            # (Optional) ProVerif library file for other properties
│     └── tls13-multiagent.pv        # ProVerif main file
│
├── binder1/                         # Analysis for binding mechanism #1
│     ├── tls-lib-simple.pvl         # ProVerif library file for correlation properties
│     ├── other-props.pvl            # (Optional) ProVerif library file for other properties
│     ├── tls13-multiagent.pv        # ProVerif main file
│     └── log.txt                    # log of ProVerif execution
│
├── binder2/                         # Analysis for binding mechanism #2
│     ├── tls-lib-simple.pvl         # ProVerif library file for correlation properties
│     ├── other-props.pvl            # (Optional) ProVerif library file for other properties
│     ├── tls13-multiagent.pv        # ProVerif main file
│     └── log.txt                    # log of ProVerif execution
│
├── binder3/                         # Analysis for binding mechanism #3
│     ├── tls-lib-simple.pvl         # ProVerif library file for correlation properties
│     ├── other-props.pvl            # (Optional) ProVerif library file for other properties
│     ├── tls13-multiagent.pv        # ProVerif main file
│     └── log.txt                    # log of ProVerif execution
│
├── binder4/                         # Analysis for binding mechanism #4
│     ├── tls-lib-simple.pvl         # ProVerif library file for correlation properties
│     ├── other-props.pvl            # (Optional) ProVerif library file for other properties
│     ├── tls13-multiagent.pv        # ProVerif main file
│     └── log.txt                    # log of ProVerif execution
│
├── binder5/                         # Analysis for binding mechanism #5
│     ├── tls-lib-simple.pvl         # ProVerif library file for correlation properties
│     ├── other-props.pvl            # (Optional) ProVerif library file for other properties
│     ├── tls13-multiagent.pv        # ProVerif main file
│     └── log.txt                    # log of ProVerif execution
│
├── binder6/                         # Analysis for binding mechanism #6
│     ├── tls-lib-simple.pvl         # ProVerif library file for correlation properties
│     ├── other-props.pvl            # (Optional) ProVerif library file for other properties
│     ├── tls13-multiagent.pv        # ProVerif main file
│     └── log.txt                    # log of ProVerif execution
│
├── binder7/                         # Analysis for binding mechanism #7
│     ├── tls-lib-simple.pvl         # ProVerif library file for correlation properties
│     ├── other-props.pvl            # (Optional) ProVerif library file for other properties
│     ├── tls13-multiagent.pv        # ProVerif main file
│     └── log.txt                    # log of ProVerif execution
│
└── proposal/                        # Analysis for our proposed binding mechanism
      ├── tls-lib-simple.pvl         # ProVerif library file for correlation properties
      ├── other-props.pvl            # (Optional) ProVerif library file for other properties
      ├── tls13-multiagent.pv        # ProVerif main file
      ├── log.txt                    # log of ProVerif execution
      └── log-optional.txt           # log of ProVerif execution for optional properties
```


## Running automatic proofs 

For completeness, optional commands for running other properties are also provided for each.

### Basic Execution
Run as follows: 

```bash 
proverif -lib tls-lib-simple.pvl tls13-multiagent.pv
```

#### With other properties
```bash 
proverif -lib tls-lib-simple.pvl -lib other-props.pvl tls13-multiagent.pv
```


### Generation of traces for failing properties
In order to additionally generate a trace for each property which results in "false", create a subfolder (e.g., `traces` in the following command) for results before executing.

```bash 
mkdir traces
```

Then to execute: run as follows:
```bash 
proverif -lib tls-lib-simple.pvl -graph traces tls13-multiagent.pv
```

OR 
```bash 
proverif -lib tls-lib-simple.pvl -html traces tls13-multiagent.pv
```

Subfolder `traces` will contain the traces in .dot as well as .PDF.

#### With other properties
```bash 
proverif -lib tls-lib-simple.pvl -lib other-props.pvl -graph traces tls13-multiagent.pv
```

OR 
```bash 
proverif -lib tls-lib-simple.pvl -lib other-props.pvl -html traces tls13-multiagent.pv
```

### Saving log
To additionally save in log file together with display:
```bash
proverif -lib tls-lib-simple.pvl -html traces tls13-multiagent.pv 2>&1 | tee log.txt
```

#### With other properties
```bash
proverif -lib tls-lib-simple.pvl -lib other-props.pvl -html traces tls13-multiagent.pv 2>&1 | tee log.txt
```

### Horn clauses
To additionally see the Horn clauses generated in ProVerif: 

a. use command-line option `-test` as follows: 
```bash
proverif -lib tls-lib-simple.pvl tls13-multiagent.pv -test
```

OR 

b. add one of the following two settings inside the input (*.pv) file:

- `set verboseClauses = short.` to display the Horn clauses

- `set verboseClauses = explained.` to additionally display a sentence after each clause it generates to explain where this clause comes from.

#### With other properties
a. use command-line option `-test` as follows: 
```bash
proverif -lib tls-lib-simple.pvl -lib other-props.pvl tls13-multiagent.pv -test
```

OR 

b. as above

### Interactive mode
To run in interactive mode:
```bash
proverif_interact -lib tls-lib-simple.pvl tls13-multiagent.pv
```

#### With other properties
```bash
proverif_interact -lib tls-lib-simple.pvl -lib other-props.pvl tls13-multiagent.pv
```

## Community Service

We shared our results with the community for review and to raise awareness on high-severity vulnerabilities and apply appropriate mitigations for the safety of their users:

### [IETF](https://www.ietf.org/)
  - [RATS WG](https://mailarchive.ietf.org/arch/msg/rats/6gbqx0XY8WYrH3Mx4vO8n2-uKgY/)
  - [SEAT WG](https://mailarchive.ietf.org/arch/msg/seat/x3eQxFjQFJLceae6l4_NgXnmsDY/)
  - [TLS WG](https://mailarchive.ietf.org/arch/msg/tls/8lyqHh9y7_Lv6b1iXhpUqYrp0M0/)
  - [LAKE WG](https://mailarchive.ietf.org/arch/msg/lake/Tovtl7wgvzwJWT2I2ZwnhoIOnYQ/)
  - [SAAG](https://mailarchive.ietf.org/arch/msg/saag/jBZVk7YySwpaFqydAfxW33kNZPY/)
  - [Practical Cybersecurity list](https://mailarchive.ietf.org/arch/msg/practical-cybersecurity/d65WPaC0WbZRwxTBclnTkf7SmRs/)
  - Agent2agent list [thread1](https://mailarchive.ietf.org/arch/msg/agent2agent/ubz7uXCs--YzuSWyXNNsmWf_tSQ/) and [thread2](https://mailarchive.ietf.org/arch/msg/agent2agent/xHhjA94fzed6ONIvPRgwTT-WRmA/)
  - [DSMC list](https://mailarchive.ietf.org/arch/msg/dmsc/QC2adIcYkxiTlniEcc7ggk86BAY/)
  - [Hackathon](https://mailarchive.ietf.org/arch/msg/hackathon/PIrJ2O_QqcNUAnMIn_Vh22ImWMc/)
  - [126attendees](https://mailarchive.ietf.org/arch/msg/126attendees/V9BKZJ_DGkZPdlnjBaUeyluhbqQ/)

### [IRTF](https://www.irtf.org/)
  - UFMRG: [thread1](https://mailarchive.ietf.org/arch/msg/ufmrg/ZWK0uMM92OdwlPbgXBvQApDpe5Q/) and [thread2](https://mailarchive.ietf.org/arch/msg/ufmrg/ZRhR7o1HrWxfGDfgRJMR65RBkDE/)
  - CFRG [thread1](https://mailarchive.ietf.org/arch/msg/cfrg/NbxHIw9H_xpSYbgfO_n7lVIFeWs/) and [thread2](https://mailarchive.ietf.org/arch/msg/cfrg/U5YHd91lYjiqCTt9BZyVDNFeUpM/)
  - [DINRG](https://mailarchive.ietf.org/arch/msg/din/_8LE3Ru1xX16hgGJwryMTRwRoaA/)

### [CCC](https://confidentialcomputing.io/)
  - Attestation SIG: [thread1](https://lists.confidentialcomputing.io/g/attestation/topic/117207133) and [thread2](https://lists.confidentialcomputing.io/g/attestation/message/334)
  - TAC: [thread1](https://lists.confidentialcomputing.io/g/tac/topic/117932193) and [thread2](https://lists.confidentialcomputing.io/g/tac/topic/120068850)

### [OCP](https://www.opencompute.org/) 
  - OCP Security: [message1](https://ocp-all.groups.io/g/OCP-Security/topic/117932716), [message2](https://ocp-all.groups.io/g/OCP-Security/topic/intra_handshake_fail/120069056), [message3](https://ocp-all.groups.io/g/OCP-Security/topic/intra_handshake_fail/120483814) and [message4](https://ocp-all.groups.io/g/OCP-Security/topic/intra_handshake_fail/120524635)

If you know any other relevant mailing list that we should inform, please let us know.

## Media Coverage
- [The Register](https://www.theregister.com/security/2026/07/04/confidential-computings-trust-mechanism-is-broken-the-fix-may-not-exist/5266056)
- (Japanese) [BlackHatNewsTokyo](https://blackhatnews.tokyo/archives/119915)
- (Several languages) [Hackernoon](https://hackernoon.com/attested-tls-was-supposed-to-be-the-last-trust-boundary-it-isnt-formal-methods-show-how)
- [Apple podcast](https://podcasts.apple.com/eg/podcast/attested-tls-was-supposed-to-be-the-last-trust/id1698517643?i=1000776623286)
- [Information Security News](https://meterpreter.org/attested-tls-vulnerability-cve-2026-33697/)
- [TheNextGenTechInsider](https://thenextgentechinsider.com/pulse/critical-flaw-discovered-in-confidential-computing-attestation-protocols)
- [DailySecurityReview](https://dailysecurityreview.com/resources/cve-2026-33697-attested-tls-relay-flaw-hits-whatsapp-cocos-ai/)
- [SC World](https://www.scworld.com/brief/confidential-computings-remote-attestation-protocol-may-have-fundamental-flaw)
- [01 Quantum](https://blogs.groupware.org.uk/01-Quantum-Inc/the-handshake-that-cant-keep-its-promise-why-confidential-computings-flaw-changes-the-data-sovereignty-conversation/)
- (Russian) [Security Lab](https://www.securitylab.ru/news/574545.php)
- (German) [blogspan](https://www.blogspan.net/confidential-computing-attestierung-relay-luecke/)
- (Chinese) [Sina](https://finance.sina.cn/tech/2026-07-04/detail-inifscxt9953361.d.html)
- [data4biz](https://data4biz.com/articles/una-falla-rompe-la-fiducia-del-confidential-computing)
- (Russian) [ITSec](https://www.itsec.ru/news/issledovateli-nashli-kriticheskuyu-uyazvimost-v-attested-tls)
- (Chinese) [smzdm](https://post.smzdm.com/p/a82ol990/)
- (Chinese) [donews](https://www.donews.com/news/detail/4/6621022.html)
- (Chinese) [ifeng](https://i.ifeng.com/c/8uUfy0PMmqE)
- [dugganusa](https://www.dugganusa.com/post/confidential-computing-s-whole-pitch-is-trust-the-proof-not-the-cloud-two-years-of-formal-verifi)
- [dugganusa repo](https://github.com/pduggusa/dugganusa-ietf/tree/main/cve-2026-33697-attestation)
- [spoitus](https://sploitus.com/exploit?id=92591A05-07BC-5015-BA3D-B1347B35D684)
- [lavx news](https://news.lavx.hu/article/attested-tls-research-exposes-a-weak-link-in-confidential-computing)
- [sohu](https://www.sohu.com/a/1045865934_122004016)
- (Persian) [news.ditty](https://news.ditty.ir/news/attested-tls-relay-flaw-formal-methods/019f6221-26ca-7293-9ee9-5557b3c0b8f8)
- (Russian) [LiMP VPN](https://limpvpn.com/ru/news/attested-tls-whatsapp-privacy-flaw-2026)
- [daily.dev](https://daily.dev/posts/kI6PoNzPx)
- [warden](https://warden.veritai.ch/news/researchers-find-attested-tls-flaws-that-weaken-confidential-computing-trust-model)
- [GCVE.eu](https://db.gcve.eu/sightings/?query=cve-2026-33697)
- [coderlegion](https://coderlegion.com/24087/intra-handshake-attestation-when-more-security-doesnt-mean-better-security)
- [Anjuna Security](https://www.anjuna.io/blog/attested-tls-flaw-explained)
- [freenode](https://freenode.net/digest/67)
- (Chinese) [csdn](https://blog.csdn.net/weixin_42376192/category_13096766.html)
- [osintsights](https://osintsights.com/confidential-computing-flaws-expose-trust-risks)
- (Turkish) [hardwaremania](https://hardwaremania.com/haber/arastirma-attested-tls-confidential-computing-icin-zayif-kaliyor/)
- [akber](https://akber.com/sovereignty-in-the-cloud-is-an-illusion/)
- [ad-hoc news](https://www.ad-hoc-news.de/wissenschaft/cloud-souveraenitaet-red-hat-startet-reifegrad-assessments-gegen/69691475)
- [AIMultiple](https://aimultiple.com/privacy-enhancing-technologies)

If you have written an article on this and would like to be added here, please send me a PR.

## Upcoming and Recent Talks and Research Visits

If you are around on any of the following venues of upcoming talks (in reverse chronological order) on topics related to the project, you are very welcome to join/meet. 

| Event/Host | Venue | Date(s) | Funding | Material |
| --- | --- | --- | --- | --- |
| [Linux Plumbers Conference 2026](https://lpc.events/event/20/) | Prague, Czechia | 5-7 Oct, 2026 | Sponsors are invited | [abstract](https://lpc.events/event/20/contributions/2585/), slides, video |
| [GA4GH 14th Plenary Meeting](https://www.ga4gh.org/event/14th-plenary/) | Singapore (Virtual) | 28 Sept-2 Oct, 2026 | - | slides, video |
| [ESORICS 2026](https://sites.google.com/di.uniroma1.it/esorics2026/) | Rome, Italy | 14-18 Sept, 2026 | Sponsors are invited | slides |
| IETF [RATS Interim meeting](https://datatracker.ietf.org/meeting/interim-2026-rats-03/session/rats) | Virtual | 14 Sept, 2026 | - | slides, video |
| Hackathon @ [RIOT Summit 2026](https://summit.riot-os.org/2026/) | Grenoble, France (Virtual) | 4 September, 2026| - | [topic synopsis](https://notes.inria.fr/2ppogr2fTSKusRog3RXbPQ?view#topic-security-analysis-of-attested-tls-and-attested-edhoc) |
| [RIOT Summit 2026](https://summit.riot-os.org/2026/) | Grenoble, France (Virtual) | 2-4 September, 2026 | - | [abstract](https://summit.riot-os.org/2026/blog/speakers/muhammad-usama-sardar/), [slides](https://www.researchgate.net/publication/413988306_Security_Analysis_of_Attested_TLS_and_Attested_EDHOC), video |
| [Data Security Work Stream (DSWS)](https://www.ga4gh.org/work_stream/data-security/) at the [Global Alliance for Genomics and Health (GA4GH)](https://www.ga4gh.org/) | Virtual | 24 Aug, 2026 | - | [slides](https://www.researchgate.net/publication/413569575_High-Severity_Vulnerabilities_in_Former_GIF_Design_for_Attested_TLS_draft-fossati-seat-early-attestation), [video](https://us02web.zoom.us/rec/share/UAn381deia-aMNmjGHhMqxocc1HcyF7ksLlaeeKefxO4bSC2mHPzwPQPYGe2dnZR.zfleYCmmtiteo_NS) |
| Confidential AI Public Side Meeting @ [IETF 126](https://www.ietf.org/meeting/126/) | Vienna, Austria | 21 July, 2026 | ULISSY s.r.l. | [plan](https://mailarchive.ietf.org/arch/msg/126attendees/odgd_xmhjQXiR_aLYdqtVvDJeF4/), [slides](https://www.researchgate.net/publication/410954219_Proposed_RG_Confidential_Computing_for_Agentic_AI), video |
| SEAT @ [IETF 126](https://www.ietf.org/meeting/126/) | Vienna, Austria | 21 July, 2026 | ULISSY s.r.l. | [slides](https://datatracker.ietf.org/meeting/126/materials/slides-126-seat-binding-properties-of-expat-00.pdf), [video](https://youtu.be/Fb5Hzh1mp1E?t=4189) |
| [IETF 126 Hackdemo Happy Hour](https://wiki.ietf.org/en/meeting/126/hackathon/hackdemo) | Vienna, Austria | 20 July, 2026 | ULISSY s.r.l. | [Hackathon project](https://wiki.ietf.org/en/meeting/126/hackathon#cve-2026-33697-cvss-75-intra-handshakefail), [demo](https://wiki.ietf.org/en/meeting/126/hackathon/hackdemo) |
| Confidential Computing Public Side Meeting @ [IETF 126](https://www.ietf.org/meeting/126/) | Vienna, Austria | 20 July, 2026 | ULISSY s.r.l. | [plan](https://mailarchive.ietf.org/arch/msg/126attendees/V9BKZJ_DGkZPdlnjBaUeyluhbqQ/), [slides](https://www.researchgate.net/publication/410954219_Proposed_RG_Confidential_Computing_for_Agentic_AI), video |
| HotRFC @ [IETF 126](https://www.ietf.org/meeting/126/) | Vienna, Austria | 19 July, 2026 | ULISSY s.r.l. | [slides](https://datatracker.ietf.org/meeting/126/materials/slides-126-hotrfc-sessa-15-confidential-computing-and-digital-sovereignty-00), [video](https://youtu.be/FDHWRijxKso?t=3285) |
| [IETF 126 Hackathon](https://www.ietf.org/meeting/hackathons/126-hackathon/) | Vienna, Austria | 19 July, 2026 | ULISSY s.r.l. | [Hackathon project](https://wiki.ietf.org/en/meeting/126/hackathon#cve-2026-33697-cvss-75-intra-handshakefail), [slides](https://datatracker.ietf.org/meeting/126/materials/slides-126-hackathon-sessd-intra-handshakefail-cve-2026-33697-00), [video](https://youtu.be/GRqyrDIEgEw?t=1340) |
| IEPG @ [IETF 126](https://www.ietf.org/meeting/126/) | Vienna, Austria | 19 July, 2026 | ULISSY s.r.l. | [slides](https://datatracker.ietf.org/meeting/126/materials/slides-126-iepg-sessa-05-intra-handshakefail-cve-2026-33697-00), [video](https://youtu.be/g8q_u19vXzk?t=4404) |
| [Workshop](https://www.wissenschaftsnacht-dresden.de/programm/detailansicht/confidential-computing-15585) @ [Dresden Science Night 2026](https://www.wissenschaftsnacht-dresden.de/en/) | Dresden | 26 June, 2026 | - | [demo](https://www.wissenschaftsnacht-dresden.de/programm/detailansicht/confidential-computing-15585) |
| [Output 2026](https://output-dd.de/) | Dresden | 25 June, 2026 | - | [demo](https://output-dd.de/projekte/relay-attacks-in-intra-handshake-attestation-for-confidential-agentic-ai-systems/) |
| [Confidential Computing Summit 2026](https://events.linuxfoundation.org/confidential-computing-summit/) (presented by Jens Albers) | San Francisco, USA | 23-24 June, 2026 | - | [poster](https://www.researchgate.net/publication/411851358_Standardization_of_Attested_TLS), video |
| [Workshop for the 25 years of ProVerif](https://bblanche.gitlabpages.inria.fr/proverif//25years.html) | Paris, France | 3 June, 2026 | Sponsors are invited | - |
| [Confidential Containers Community Meeting](https://confidentialcontainers.org/) @ [Cloud Native Computing Foundation](https://www.cncf.io/) | Virtual | 30 April, 2026 | - | [slides](https://www.researchgate.net/publication/411849492_Relay_Attacks_in_Intra-handshake_Attestation), [video](https://zoom.us/rec/share/3thZhsRi-BZJL-GqjnwGzh7inbltuKIlpVjqMlWp6WRdMTZ66Z8p-8YjaaeOfbhX.CoH6YBukaKua0gkt) around timestamp 00:27:00 |
| GIF Project showcase @ [GA4GH April Connect 2026](https://www.ga4gh.org/event/april-connect-2026/) | Montreal, Canada (virtual) | 17 April, 2026 | - | [slides](https://www.researchgate.net/publication/412136610_Trusted_Research_Environment_TRE_Open_Suite), [video](https://youtu.be/Kr9oxp1fdn0?t=1083), [report](https://www.ga4gh.org/document/arpril-connect-2026-meeting-report/) |
| [NSA Symposium on Hot Topics in the Science of Security (HotSoS) 2026](https://sos-vo.org/group/hotsos/) | Virtual | 16 April, 2026 | - | [abstract](https://sos-vo.org/group/hotsos/2026/sardar), [slides](https://sos-vo.org/system/files/2026-04/20260416_HotSoS%20%281%29.pdf), [video](https://sos-vo.org/group/hotsos/2026/sardar) |
| [PET-CON 2026.1: 15th Privacy Enhancing Techniques Convention](https://fg-pet.gi.de/veranstaltung/15th-privacy-enhancing-techniques-convention) | Karlsruhe, Germany | 16-17 April, 2026 | Sponsors are invited | [slides](https://www.researchgate.net/publication/411849502_Formal_Analysis_of_Attested_TLS), [poster](https://www.researchgate.net/publication/411852738_Formal_Analysis_of_Attested_TLS_and_Standardization_in_the_IETF) |
| [GTMFS 2026: Annual Meeting of the WG "Formal Methods in Security"](https://gtmfs2026.sciencesconf.org/program?lang=en) | Luz-Saint-Sauveur, France | 24-26 Mar, 2026 | Sponsors are invited | [slides](https://www.researchgate.net/publication/411853715_Relay_Attacks_in_Intra-handshake_Attestation) |
| TLS @ [IETF 125](https://www.ietf.org/meeting/125/) | Shenzhen, China (virtual) | 20 Mar, 2026 | - | [slides](https://datatracker.ietf.org/meeting/125/materials/slides-125-tls-tls-fatt-extensions-00), [video](https://youtu.be/2GkmQmRlkto?t=3988) |
| CFRG @ [IETF 125](https://www.ietf.org/meeting/125/) | Shenzhen, China (virtual) | 19 Mar, 2026 | - | [slides](https://datatracker.ietf.org/meeting/125/materials/slides-125-cfrg-relay-attacks-00), [video](https://youtu.be/IfKgbO74Lt4?t=6054) |
| SEAT @ [IETF 125](https://www.ietf.org/meeting/125/) (expat) | Shenzhen, China (virtual) | 17 Mar, 2026 | - | [slides](https://datatracker.ietf.org/meeting/125/materials/slides-125-seat-seat-expat-00), [video](https://youtu.be/hX7genEkN7w?t=3169) |
| SEAT @ [IETF 125](https://www.ietf.org/meeting/125/) (relay) | Shenzhen, China (virtual) | 17 Mar, 2026 | - | [slides](https://datatracker.ietf.org/meeting/125/materials/slides-125-seat-security-analysis-00), [video](https://youtu.be/hX7genEkN7w?t=676) |
| Side meeting @ [IETF 125](https://www.ietf.org/meeting/125/) | Shenzhen, China (virtual) | 16 Mar, 2026 | - | [slides](https://www.researchgate.net/publication/403474373_Proposed_RG_Confidential_AI) |
| LAKE @ [IETF 125](https://www.ietf.org/meeting/125/) | Shenzhen, China (virtual) | 16 Mar, 2026 | - | [slides](https://datatracker.ietf.org/meeting/125/materials/slides-125-lake-formal-analysis-of-attested-edhoc-00), [video](https://youtu.be/JzfLpbnhl0A?t=3117) |
| HotRFC @ [IETF 125](https://www.ietf.org/meeting/125/) | Shenzhen, China (virtual) | 15 Mar, 2026 | - | [slides](https://datatracker.ietf.org/meeting/125/materials/slides-125-hotrfc-sessa-formal-proof-of-insecurity-of-intra-handshake-attestation-00), [video](https://youtu.be/OtOo7Nogisw?t=3514) |
| [IETF 125 Hackathon](https://www.ietf.org/meeting/hackathons/125-hackathon/) | Shenzhen, China (virtual) | 14-15 Mar, 2026 | - | [Hackathon project](https://wiki.ietf.org/en/meeting/125/hackathon#relay-attacks-in-intra-handshake-attestation-for-confidential-agentic-ai-systems), [slides](https://datatracker.ietf.org/meeting/125/materials/slides-125-hackathon-sessd-relay-attacks-in-intra-handshake-attestation-00), [video](https://youtu.be/62A58qH19MI?t=2270) |
| [Open Confidential Computing Conference (OC3)](https://www.oc3.dev/) | Berlin  | 12 Mar, 2026 | - | - |
| [CCC Attestation SIG](https://github.com/CCC-Attestation) | Virtual | 10 Feb, 2026 | - | [slides](https://github.com/muhammad-usama-sardar/CCC-Att-meetings/blob/main/materials/MuhammadUsamaSardar_RelayAttacksGen_20260210.pdf); [video](https://www.youtube.com/watch?v=idqwb0hFlhs&list=PLmfkUJc39uMhZsNGmpx-qD-uCoQyMglIp&t=1061s) |
| [IETF RATS Interim meeting](https://datatracker.ietf.org/meeting/interim-2026-rats-01/session/rats) | Virtual | 9 Feb, 2026 | - | [slides](https://datatracker.ietf.org/meeting/interim-2026-rats-01/materials/slides-interim-2026-rats-01-sessa-relayattacks-00.pdf), [video](https://youtu.be/gURY61dViPw?t=1474)  |
| [Confidential Computing](https://fosdem.org/2026/schedule/track/confidential-computing/) devroom at [FOSDEM 2026](https://fosdem.org/2026/) | Brussels, Belgium | 31 Jan-1 Feb, 2026 | [CCC](https://confidentialcomputing.io/) | [abstract](https://fosdem.org/2026/schedule/event/GHGFBM-attestedtls/), [slides](https://fosdem.org/2026/events/attachments/GHGFBM-attestedtls/slides/267432/20260201_60u9e0n.pdf), [video](https://video.fosdem.org/2026/ud6215/GHGFBM-attestedtls.av1.webm) |
| [CCC Attestation SIG](https://github.com/CCC-Attestation) | Virtual | 27 Jan, 2026 | - | [slides](https://github.com/muhammad-usama-sardar/CCC-Att-meetings/blob/main/materials/MuhammadUsamaSardar_RelayAttacksProposal_20260127.pdf); [video](https://youtu.be/P04tLJcSxfM?list=PLmfkUJc39uMhZsNGmpx-qD-uCoQyMglIp&t=434) |
| [CCC Attestation SIG](https://github.com/CCC-Attestation) | Virtual | 13 Jan, 2026 | - | [slides](https://github.com/muhammad-usama-sardar/CCC-Att-meetings/blob/main/materials/MuhammadUsamaSardar_RelayAttacks_20260113.pdf); [video](https://youtu.be/cSrCZNyo7_g?list=PLmfkUJc39uMhZsNGmpx-qD-uCoQyMglIp&t=1083) |
| [CCC Attestation SIG](https://github.com/CCC-Attestation) | Virtual | 16 Dec, 2025 | - | [slides](https://github.com/CCC-Attestation/meetings/blob/main/materials/MuhammadUsamaSardar_Binding_Properties_20251216.pdf); [video](https://youtu.be/w_MrjMeHyP8?list=PLmfkUJc39uMhZsNGmpx-qD-uCoQyMglIp&t=593) |
| [CCC Attestation SIG](https://github.com/CCC-Attestation) | Virtual | 2 Dec, 2025 | - | [slides](https://github.com/muhammad-usama-sardar/CCC-Att-meetings/blob/main/materials/MuhammadUsamaSardar_Open_Questions_20251202.pdf); [video](https://youtu.be/16aGZ-oZidg?list=PLmfkUJc39uMhZsNGmpx-qD-uCoQyMglIp&t=2920) |

## Feedback/Comments/Critique/Contributions
We would love to have your contributions and feedback (especially critique! yes, this is how the science progresses, but please be genuine!). Contact Muhammad Usama Sardar by [email](https://tu-dresden.de/ing/informatik/sya/se/die-professur/beschaeftigte/muhammad-usama-sardar), submit a **minimal** PR, or open an issue. For your contribution to be dealt promptly, please consider the following remarks:

**Remark 1**. This is an official repo of [Intra-handshake.fail paper](https://www.researchgate.net/publication/408219182_Intra-handshakefail_CVE-2026-33697_High-severity_CVE_in_Attested_TLS). Not everything about attested TLS (and even intra-handshake attestation) needs to be put into this repo. The paper has a specific scope, and everything out of scope has to be dealt with outside of this repo. If you are unsure, please drop an email to discuss.

**Remark 2**. This paper is based on the work that concluded around December 2025. Please see [vulnerability disclosure report](https://mailarchive.ietf.org/arch/msg/seat/x3eQxFjQFJLceae6l4_NgXnmsDY/) to the IETF on 11 Jan, 2026 as evidence. A huge amount of follow-up work has been done in the past months. Some of that is under submission; some of that is in progress for submission. If the contents of your PR are already answered by those papers, it will not be merged in this repo. As all of our previous work is available under the Apache-2.0 License, we remain fully committed to making the artifacts from those papers open source under the same license for reproducibility, extensibility, and further research.

**Remark 3**. ESORICS has a strict page limit. A total of 20 pages are allowed. A single word over that is desk rejected (including Appendix; it happened with us before). We could put only a limited number of things in 20 pages, while keeping it still readable. Please explain clearly and precisely how your question and/or concern relates to the paper.

**Remark 4**. If your proposed code changes the formal model, threat model, and properties, it has to be supported with strong evidence. The reviewers have reviewed a specific formal model, threat model, and properties. Changing those settings is not fair.

**Remark 5**. Huge PRs are very unlikely to be merged. Multiple small, precise, concise and to-the-point PRs are much appreciated and more likely to find their way to be merged.

**Remark 6**. Please indicate any usage of AI-assistance upfront. 

**Remark 7**. The acknowledgment list for this repo is locked as the camera-ready version for ESORICS has been submitted. Any further contributions or discussions that the authors find insightful and helpful would be acknowledged in the [draft](https://datatracker.ietf.org/doc/draft-intra-handshake-fail/).

**Remark 8**. Please be aware that we are currently dealing with several critical (up to 9.8 CVSS) CVEs in intra-handshake attestation. Please keep your contributions focused on the most urgent items. If you do not respond to our questions, your PR will not be merged.

**Remark 9**. If possible, please review the [extensive discussion in IETF/IRTF](https://www.ietf.org/archive/id/draft-intra-handshake-fail-21.html#section-16.2) and the threads before submitting an issue. If you raise an issue that has been discussed there, we can only refer you back to those discussions.

**Remark 10**. Disputes are welcome. Please first quote the statement from the paper that you dispute. Then present your rationale of why you believe the statement is wrong. Please be as precise and concise as possible.

**Remark 11**. Remote attestation is a very heated topic. Please be respectful.