---
title: ai.gnus.sdk.KeyStoreHelper

---

# ai.gnus.sdk.KeyStoreHelper





## Public Functions

|                | Name           |
| -------------- | -------------- |
| void | **[initialize](/source-reference/Classes/d0/d1b/classai_1_1gnus_1_1sdk_1_1_key_store_helper/#function-initialize)**(Context context) |
| boolean | **[isInitialized](/source-reference/Classes/d0/d1b/classai_1_1gnus_1_1sdk_1_1_key_store_helper/#function-isinitialized)**() |
| String | **[load](/source-reference/Classes/d0/d1b/classai_1_1gnus_1_1sdk_1_1_key_store_helper/#function-load)**() |
| boolean | **[save](/source-reference/Classes/d0/d1b/classai_1_1gnus_1_1sdk_1_1_key_store_helper/#function-save)**(String data) |
| boolean | **[delete](/source-reference/Classes/d0/d1b/classai_1_1gnus_1_1sdk_1_1_key_store_helper/#function-delete)**(String key) |

## Public Functions Documentation

### function initialize

```java
public static void initialize(
    Context context
)
```


Initialize the [KeyStoreHelper](/source-reference/Classes/d0/d1b/classai_1_1gnus_1_1sdk_1_1_key_store_helper/) with application context. Must be called once before using load/save/delete methods. Typically called in Application.onCreate() 


### function isInitialized

```java
public static boolean isInitialized()
```


Check if [KeyStoreHelper](/source-reference/Classes/d0/d1b/classai_1_1gnus_1_1sdk_1_1_key_store_helper/) has been initialized. 


### function load

```java
public static String load()
```


### function save

```java
public static boolean save(
    String data
)
```


### function delete

```java
public static boolean delete(
    String key
)
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700