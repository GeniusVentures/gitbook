---
title: sgns::ValidatorRegistry::WeightConfig
summary: Weight policy used to score validators and update penalties. 

---

# sgns::ValidatorRegistry::WeightConfig



Weight policy used to score validators and update penalties. 


`#include <ValidatorRegistry.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| uint64_t | **[genesis_weight_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-genesis_weight_)** <br/>Base weight for genesis authority validators.  |
| uint64_t | **[full_weight_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-full_weight_)** <br/>Base weight for full validators.  |
| uint64_t | **[regular_weight_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-regular_weight_)** <br/>Base weight for regular validators.  |
| uint64_t | **[sharded_weight_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-sharded_weight_)** <br/>Base weight for sharded validators.  |
| uint64_t | **[genesis_max_weight_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-genesis_max_weight_)** <br/>Max weight allowed for genesis validators.  |
| uint64_t | **[full_max_weight_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-full_max_weight_)** <br/>Max weight allowed for full validators.  |
| uint64_t | **[regular_max_weight_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-regular_max_weight_)** <br/>Max weight allowed for regular validators.  |
| uint64_t | **[sharded_max_weight_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-sharded_max_weight_)** <br/>Max weight allowed for sharded validators.  |
| uint64_t | **[approval_increment_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-approval_increment_)** <br/>Weight increment applied for approved behavior.  |
| uint32_t | **[penalty_threshold_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-penalty_threshold_)** <br/>Penalty score threshold before harsher actions.  |
| uint32_t | **[penalty_cap_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-penalty_cap_)** <br/>Maximum accumulated penalty score.  |
| uint32_t | **[blacklist_bump_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-blacklist_bump_)** <br/>Penalty increment applied for severe failures.  |
| uint32_t | **[missed_epoch_threshold_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-missed_epoch_threshold_)** <br/>Missed-epoch threshold used for inactivity decisions.  |
| uint32_t | **[inactivity_decrement_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-inactivity_decrement_)** <br/>Weight decrement for inactive validators.  |
| uint64_t | **[total_weight_cap_multiplier_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-total_weight_cap_multiplier_)** <br/>Multiplier controlling global weight-cap normalization.  |
| uint64_t | **[certificate_timestamp_window_ms_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-certificate_timestamp_window_ms_)** <br/>Allowed timestamp drift for certificates.  |
| uint64_t | **[slot_direct_numerator_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-slot_direct_numerator_)** <br/>Slot 0 (DIRECT_API) weight numerator. 0.50 = 1/2 (D-02).  |
| uint64_t | **[slot_direct_denominator_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-slot_direct_denominator_)** <br/>Slot 0 (DIRECT_API) weight denominator. 0.50 = 1/2 (D-02).  |
| uint64_t | **[slot_public_numerator_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-slot_public_numerator_)** <br/>Slots 1-2 (PUBLIC) weight numerator. 0.25 = 1/4 (D-03).  |
| uint64_t | **[slot_public_denominator_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-slot_public_denominator_)** <br/>Slots 1-2 (PUBLIC) weight denominator. 0.25 = 1/4 (D-03).  |
| uint64_t | **[slot_quorum_numerator_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-slot_quorum_numerator_)** <br/>Cumulative quorum threshold numerator. 0.75 = 3/4 (D-06).  |
| uint64_t | **[slot_quorum_denominator_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-slot_quorum_denominator_)** <br/>Cumulative quorum threshold denominator.0.75 = 3/4 (D-06).  |
| uint64_t | **[slot_public_min_group_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-slot_public_min_group_)** <br/>D-03: minimum distinct validators per PUBLIC hash group.  |
| uint64_t | **[full_promotion_weight_](/source-reference/Classes/dd/d71/structsgns_1_1_validator_registry_1_1_weight_config/#variable-full_promotion_weight_)** <br/>Weight at which a REGULAR validator is promoted to FULL (D-08).  |

## Public Attributes Documentation

### variable genesis_weight_

```cpp
uint64_t genesis_weight_ = 50000;
```

Base weight for genesis authority validators. 

### variable full_weight_

```cpp
uint64_t full_weight_ = 1000;
```

Base weight for full validators. 

### variable regular_weight_

```cpp
uint64_t regular_weight_ = 1;
```

Base weight for regular validators. 

### variable sharded_weight_

```cpp
uint64_t sharded_weight_ = 1;
```

Base weight for sharded validators. 

### variable genesis_max_weight_

```cpp
uint64_t genesis_max_weight_ = 50000;
```

Max weight allowed for genesis validators. 

### variable full_max_weight_

```cpp
uint64_t full_max_weight_ = 5000;
```

Max weight allowed for full validators. 

### variable regular_max_weight_

```cpp
uint64_t regular_max_weight_ = 100;
```

Max weight allowed for regular validators. 

### variable sharded_max_weight_

```cpp
uint64_t sharded_max_weight_ = 100;
```

Max weight allowed for sharded validators. 

### variable approval_increment_

```cpp
uint64_t approval_increment_ = 1;
```

Weight increment applied for approved behavior. 

### variable penalty_threshold_

```cpp
uint32_t penalty_threshold_ = 10;
```

Penalty score threshold before harsher actions. 

### variable penalty_cap_

```cpp
uint32_t penalty_cap_ = 100;
```

Maximum accumulated penalty score. 

### variable blacklist_bump_

```cpp
uint32_t blacklist_bump_ = 10;
```

Penalty increment applied for severe failures. 

### variable missed_epoch_threshold_

```cpp
uint32_t missed_epoch_threshold_ = 500;
```

Missed-epoch threshold used for inactivity decisions. 

### variable inactivity_decrement_

```cpp
uint32_t inactivity_decrement_ = 1;
```

Weight decrement for inactive validators. 

### variable total_weight_cap_multiplier_

```cpp
uint64_t total_weight_cap_multiplier_ = 4;
```

Multiplier controlling global weight-cap normalization. 

### variable certificate_timestamp_window_ms_

```cpp
uint64_t certificate_timestamp_window_ms_ = 300000;
```

Allowed timestamp drift for certificates. 

### variable slot_direct_numerator_

```cpp
uint64_t slot_direct_numerator_ = 1;
```

Slot 0 (DIRECT_API) weight numerator. 0.50 = 1/2 (D-02). 

### variable slot_direct_denominator_

```cpp
uint64_t slot_direct_denominator_ = 2;
```

Slot 0 (DIRECT_API) weight denominator. 0.50 = 1/2 (D-02). 

### variable slot_public_numerator_

```cpp
uint64_t slot_public_numerator_ = 1;
```

Slots 1-2 (PUBLIC) weight numerator. 0.25 = 1/4 (D-03). 

### variable slot_public_denominator_

```cpp
uint64_t slot_public_denominator_ = 4;
```

Slots 1-2 (PUBLIC) weight denominator. 0.25 = 1/4 (D-03). 

### variable slot_quorum_numerator_

```cpp
uint64_t slot_quorum_numerator_ = 3;
```

Cumulative quorum threshold numerator. 0.75 = 3/4 (D-06). 

### variable slot_quorum_denominator_

```cpp
uint64_t slot_quorum_denominator_ = 4;
```

Cumulative quorum threshold denominator.0.75 = 3/4 (D-06). 

### variable slot_public_min_group_

```cpp
uint64_t slot_public_min_group_ = 2;
```

D-03: minimum distinct validators per PUBLIC hash group. 

### variable full_promotion_weight_

```cpp
uint64_t full_promotion_weight_ = 500;
```

Weight at which a REGULAR validator is promoted to FULL (D-08). 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700