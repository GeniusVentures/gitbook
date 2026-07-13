---
title: sgns::crdt::CRDTDataFilter

---

# sgns::crdt::CRDTDataFilter






`#include <crdt_data_filter.hpp>`

## Public Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[FilterCallbackEntry](/source-reference/Classes/df/d7c/structsgns_1_1crdt_1_1_c_r_d_t_data_filter_1_1_filter_callback_entry/)**  |

## Public Types

|                | Name           |
| -------------- | -------------- |
| using std::function< std::optional< std::vector< pb::Element > >(const pb::Element &)> | **[ElementFilterCallback](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/#using-elementfiltercallback)** <br/>Element filtering callback definition.  |
| using std::vector< std::shared_ptr< const [FilterCallbackEntry](/source-reference/Classes/df/d7c/structsgns_1_1crdt_1_1_c_r_d_t_data_filter_1_1_filter_callback_entry/) > > | **[FilterCallbackRegistry](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/#using-filtercallbackregistry)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[CRDTDataFilter](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/#function-crdtdatafilter)**(std::shared_ptr< [CRDTWorkJournal](/source-reference/Classes/d9/dc9/classsgns_1_1crdt_1_1_c_r_d_t_work_journal/) > work_journal, bool accept_by_default =true)<br/>Construct a new [CRDTDataFilter](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/) object.  |
| | **[~CRDTDataFilter](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/#function-~crdtdatafilter)**() =default<br/>Destroy the [CRDTDataFilter](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/) object.  |
| bool | **[RegisterElementFilter](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/#function-registerelementfilter)**(const std::string & pattern, [ElementFilterCallback](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/#using-elementfiltercallback) filter)<br/>Registers an element filter callback.  |
| bool | **[RegisterTombstoneFilter](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/#function-registertombstonefilter)**(const std::string & pattern, [ElementFilterCallback](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/#using-elementfiltercallback) filter)<br/>Registers a tombstone filter callback.  |
| void | **[UnregisterElementFilter](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/#function-unregisterelementfilter)**(const std::string & pattern)<br/>Removes the registration of an element filter that corresponds to a pattern.  |
| void | **[UnregisterTombstoneFilter](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/#function-unregistertombstonefilter)**(const std::string & pattern)<br/>Removes the registration of a tombstone filter that corresponds to a pattern.  |
| void | **[FilterElementsOnDelta](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/#function-filterelementsondelta)**(pb::Delta & delta) const<br/>Tries to filter the elements on delta according to stored filters.  |
| void | **[FilterTombstonesOnDelta](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/#function-filtertombstonesondelta)**(pb::Delta & delta)<br/>Tries to filter the tombstones on delta according to stored filters.  |

## Public Types Documentation

### using ElementFilterCallback

```cpp
using sgns::crdt::CRDTDataFilter::ElementFilterCallback = std::function<std::optional<std::vector<pb::Element>>( const pb::Element & )>;
```

Element filtering callback definition. 

### using FilterCallbackRegistry

```cpp
using sgns::crdt::CRDTDataFilter::FilterCallbackRegistry = std::vector<std::shared_ptr<const FilterCallbackEntry>>;
```


## Public Functions Documentation

### function CRDTDataFilter

```cpp
explicit CRDTDataFilter(
    std::shared_ptr< CRDTWorkJournal > work_journal,
    bool accept_by_default =true
)
```

Construct a new [CRDTDataFilter](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/) object. 

**Parameters**: 

  * **accept_by_default** if true, every delta that doesn't have a filter gets accepted. if false, rejects by default. 


### function ~CRDTDataFilter

```cpp
~CRDTDataFilter() =default
```

Destroy the [CRDTDataFilter](/source-reference/Classes/dd/d9b/classsgns_1_1crdt_1_1_c_r_d_t_data_filter/) object. 

### function RegisterElementFilter

```cpp
bool RegisterElementFilter(
    const std::string & pattern,
    ElementFilterCallback filter
)
```

Registers an element filter callback. 

**Parameters**: 

  * **pattern** The regex/pattern that the key of the element has to match 
  * **filter** The callback that is executed in case the pattern matches 


**Return**: true if succeeded, false otherwise 

### function RegisterTombstoneFilter

```cpp
bool RegisterTombstoneFilter(
    const std::string & pattern,
    ElementFilterCallback filter
)
```

Registers a tombstone filter callback. 

**Parameters**: 

  * **pattern** The regex/pattern that the key of the tombstone has to match 
  * **filter** The callback that is executed in case the pattern matches 


**Return**: true if succeeded, false otherwise 

### function UnregisterElementFilter

```cpp
void UnregisterElementFilter(
    const std::string & pattern
)
```

Removes the registration of an element filter that corresponds to a pattern. 

**Parameters**: 

  * **pattern** The regex/pattern that the key of the element has to match 


### function UnregisterTombstoneFilter

```cpp
void UnregisterTombstoneFilter(
    const std::string & pattern
)
```

Removes the registration of a tombstone filter that corresponds to a pattern. 

**Parameters**: 

  * **pattern** The regex/pattern that the key of the tombstone has to match 


### function FilterElementsOnDelta

```cpp
void FilterElementsOnDelta(
    pb::Delta & delta
) const
```

Tries to filter the elements on delta according to stored filters. 

**Parameters**: 

  * **delta** The delta to be filtered 


### function FilterTombstonesOnDelta

```cpp
void FilterTombstonesOnDelta(
    pb::Delta & delta
)
```

Tries to filter the tombstones on delta according to stored filters. 

**Parameters**: 

  * **delta** The delta to be filtered 


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700