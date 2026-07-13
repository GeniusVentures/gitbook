---
title: sgns::ValidatorRegistry::CertificateVotes
summary: Partitioned vote extraction from a certificate. 

---

# sgns::ValidatorRegistry::CertificateVotes



Partitioned vote extraction from a certificate. 

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::unordered_set< std::string > | **[approved](/source-reference/Classes/d8/dd7/structsgns_1_1_validator_registry_1_1_certificate_votes/#variable-approved)** <br/>Validators that approved the certificate.  |
| std::unordered_set< std::string > | **[unregistered](/source-reference/Classes/d8/dd7/structsgns_1_1_validator_registry_1_1_certificate_votes/#variable-unregistered)** <br/>Unregistered voters observed in certificate.  |
| std::unordered_map< std::string, bool > | **[registered_votes](/source-reference/Classes/d8/dd7/structsgns_1_1_validator_registry_1_1_certificate_votes/#variable-registered_votes)** <br/>Vote decisions by registered validators.  |
| std::unordered_map< std::string, bool > | **[unregistered_votes](/source-reference/Classes/d8/dd7/structsgns_1_1_validator_registry_1_1_certificate_votes/#variable-unregistered_votes)** <br/>Vote decisions by unregistered validators.  |

## Public Attributes Documentation

### variable approved

```cpp
std::unordered_set< std::string > approved;
```

Validators that approved the certificate. 

### variable unregistered

```cpp
std::unordered_set< std::string > unregistered;
```

Unregistered voters observed in certificate. 

### variable registered_votes

```cpp
std::unordered_map< std::string, bool > registered_votes;
```

Vote decisions by registered validators. 

### variable unregistered_votes

```cpp
std::unordered_map< std::string, bool > unregistered_votes;
```

Vote decisions by unregistered validators. 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700