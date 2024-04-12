# Regulations & Compliances

<h3>Table of Contents</h3>

[TOC]

# GDPR

EU's General Data Protection Regulation.

A European law that established protections for privacy and security of personal data about individuals in European Economic Area (“EEA”).

- https://www.gdpreu.org/the-regulation/
- PII anonymization
- applicable to
    - Companies that do business in the European Union (EU) or European Economic Area (EEA) 

Ref:

- https://www.gdpreu.org/the-regulation/key-concepts/personal-data/
- https://linfordco.com/blog/gdpr-soc-2/

# CCPA

California Consumer Protection Act 

- https://oag.ca.gov/privacy/ccpa
- PII de-identification
- applicable to
    - Companies that do business in the United States of America 

Ref:
- https://www.termsfeed.com/blog/ccpa/


# GDPR vs CCPA

- https://www.termsfeed.com/blog/gdpr-anonymization-versus-ccpa-de-identification/

# SOC2

System & Organization Control

https://soc2.co.uk/
https://en.wikipedia.org/wiki/System_and_Organization_Controls


- https://cloud.google.com/security/compliance/soc-2
- https://www.onelogin.com/compliance/soc-2-type-2
- https://linfordco.com/blog/gdpr-soc-2/


# Type of Data

## Personal Data (PII)

## Pseudonymous Data

## Anonymous Data

# PII Anonymization/Deidentification Techniques

- https://help.branch.io/using-branch/docs/best-practices-to-avoid-sending-pii-to-branch
- Hashing of personally identifiable information is not sufficient
    - https://www.johndcook.com/blog/2019/07/20/hashing-pii-does-not-protect-privacy/
    - https://dl.gi.de/handle/20.500.12116/16294
        - https://dl.gi.de/bitstream/handle/20.500.12116/16294/sicherheit2018-04.pdf?sequence=1&isAllowed=y
    - quantum computing
        - https://medium.com/meeco/why-hashed-personally-identifiable-information-pii-on-the-blockchain-can-be-safe-b842357b9663
- https://blog.littledata.io/2016/08/03/personally-identifiable-information-pii-hashing-and-google-analytics/
- https://www.imperva.com/learn/data-security/data-obfuscation/
- https://arstechnica.com/information-technology/2013/05/how-crackers-make-minced-meat-out-of-your-passwords/

- sha256 hashing is ideal
- ways to increase the effort of an attacker
    - choose slow algo
    - use salt/padding

## Data Masking
- replace the PII with general values, which are still unique
