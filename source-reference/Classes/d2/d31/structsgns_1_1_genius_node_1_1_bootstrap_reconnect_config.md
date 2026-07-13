---
title: sgns::GeniusNode::BootstrapReconnectConfig

---

# sgns::GeniusNode::BootstrapReconnectConfig





## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::chrono::seconds | **[base_delay](/source-reference/Classes/d2/d31/structsgns_1_1_genius_node_1_1_bootstrap_reconnect_config/#variable-base_delay)**  |
| std::chrono::seconds | **[max_delay](/source-reference/Classes/d2/d31/structsgns_1_1_genius_node_1_1_bootstrap_reconnect_config/#variable-max_delay)**  |
| std::chrono::seconds | **[health_check_interval](/source-reference/Classes/d2/d31/structsgns_1_1_genius_node_1_1_bootstrap_reconnect_config/#variable-health_check_interval)**  |
| std::chrono::seconds | **[health_check_disconnected_interval](/source-reference/Classes/d2/d31/structsgns_1_1_genius_node_1_1_bootstrap_reconnect_config/#variable-health_check_disconnected_interval)**  |
| double | **[background_multiplier](/source-reference/Classes/d2/d31/structsgns_1_1_genius_node_1_1_bootstrap_reconnect_config/#variable-background_multiplier)**  |

## Public Attributes Documentation

### variable base_delay

```cpp
std::chrono::seconds base_delay { 5 };
```


### variable max_delay

```cpp
std::chrono::seconds max_delay { 300 };
```


### variable health_check_interval

```cpp
std::chrono::seconds health_check_interval { 60 };
```


### variable health_check_disconnected_interval

```cpp
std::chrono::seconds health_check_disconnected_interval { 15 };
```


### variable background_multiplier

```cpp
double background_multiplier { 3.0 };
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700