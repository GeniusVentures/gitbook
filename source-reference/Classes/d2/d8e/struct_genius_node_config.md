---
title: GeniusNodeConfig
summary: Runtime configuration values used to bootstrap a Genius node instance. 

---

# GeniusNodeConfig



Runtime configuration values used to bootstrap a Genius node instance. 


`#include <GeniusNode.hpp>`

## Public Attributes

|                | Name           |
| -------------- | -------------- |
| std::string | **[Addr](/source-reference/Classes/d2/d8e/struct_genius_node_config/#variable-addr)** <br/>Developer payout address.  |
| std::string | **[Cut](/source-reference/Classes/d2/d8e/struct_genius_node_config/#variable-cut)** <br/>Developer or peer cut encoded as a string.  |
| std::string | **[TokenValueInGNUS](/source-reference/Classes/d2/d8e/struct_genius_node_config/#variable-tokenvalueingnus)** <br/>Conversion rate used for child-token.  |
| [sgns::TokenID](/source-reference/Classes/d9/dd1/classsgns_1_1_token_i_d/) | **[TokenID](/source-reference/Classes/d2/d8e/struct_genius_node_config/#variable-tokenid)** <br/>Child token identifier configured for this node.  |
| std::string | **[BaseWritePath](/source-reference/Classes/d2/d8e/struct_genius_node_config/#variable-basewritepath)** <br/>Base directory for node databases, logs, and account storage.  |
| [sgns::ChainlistFetcher](/source-reference/Namespaces/d2/d2b/namespacesgns/#using-chainlistfetcher) | **[chainlist_fetcher](/source-reference/Classes/d2/d8e/struct_genius_node_config/#variable-chainlist_fetcher)** <br/>Optional: injected chainlist source (nullptr → fetch from network).  |

## Public Attributes Documentation

### variable Addr

```cpp
std::string Addr;
```

Developer payout address. 

### variable Cut

```cpp
std::string Cut;
```

Developer or peer cut encoded as a string. 

### variable TokenValueInGNUS

```cpp
std::string TokenValueInGNUS;
```

Conversion rate used for child-token. 

### variable TokenID

```cpp
sgns::TokenID TokenID;
```

Child token identifier configured for this node. 

### variable BaseWritePath

```cpp
std::string BaseWritePath;
```

Base directory for node databases, logs, and account storage. 

### variable chainlist_fetcher

```cpp
sgns::ChainlistFetcher chainlist_fetcher {};
```

Optional: injected chainlist source (nullptr → fetch from network). 

-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700