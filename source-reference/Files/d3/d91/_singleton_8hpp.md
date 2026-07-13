---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/singleton/Singleton.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/singleton/Singleton.hpp





## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[CSingleton](/source-reference/Classes/de/daf/class_c_singleton/)**  |

## Attributes

|                | Name           |
| -------------- | -------------- |
| bool | **[CSingleton< T >::isInitialized](/source-reference/Files/d3/d91/_singleton_8hpp/#variable-csingleton<-t->isinitialized)**  |
| T * | **[CSingleton< T >::_instance](/source-reference/Files/d3/d91/_singleton_8hpp/#variable-csingleton<-t->_instance)**  |

## Defines

|                | Name           |
| -------------- | -------------- |
|  | **[SINGLETONINSTANCE](/source-reference/Files/d3/d91/_singleton_8hpp/#define-singletoninstance)**(T)  |
|  | **[SINGLETON](/source-reference/Files/d3/d91/_singleton_8hpp/#define-singleton)**(T)  |
|  | **[SINGLETONCONSTRUCTOROVERRIDE](/source-reference/Files/d3/d91/_singleton_8hpp/#define-singletonconstructoroverride)**(T)  |



## Attributes Documentation

### variable CSingleton< T >::isInitialized

```cpp
bool CSingleton< T >::isInitialized = false;
```


### variable CSingleton< T >::_instance

```cpp
T * CSingleton< T >::_instance = NULL;
```



## Macros Documentation

### define SINGLETONINSTANCE

```cpp
#define SINGLETONINSTANCE(
    T
)
CSingleton< T >::Instance()
```


### define SINGLETON

```cpp
#define SINGLETON(
    T
)
protected:                                      \
    friend class CSingleton< T >;               \
    T(T *) {}                                   \
    T(){}
```


### define SINGLETONCONSTRUCTOROVERRIDE

```cpp
#define SINGLETONCONSTRUCTOROVERRIDE(
    T
)
protected:                                      \
    friend class CSingleton< T >;               \
    T(T *) {}
```


## Source code

```cpp
//---------------------------------------------------------------------
// File:        Singleton.hpp
// Description: template for Singleton objects
// Created:     11/30/03
// Author:      Kenneth L. Hurley
//---------------------------------------------------------------------

#ifndef SINGLETON_H
#define SINGLETON_H

//
// this code is so that object can register themselves with
// the system.
//

template <class T>
class CSingleton 
{
private:
    static bool isInitialized;
    static T *_instance;                  // first initialize memory without constructor
public:
    static T *Instance()
    {
        // start lock for multithreading here
        if (_instance == NULL)
        {
            _instance = new T(_instance);
        }
        
        if (!isInitialized)
        {
            isInitialized = true;
            new (_instance) T();
        }
        return _instance;
    }; 

private: 
    CSingleton() {}; 
    ~CSingleton() {};
    // disable copy & assignment
    CSingleton( CSingleton const&);
    CSingleton& operator=( CSingleton const&);
};

template <class T>
bool CSingleton<T>::isInitialized = false;

template <class T>
T *CSingleton<T>::_instance = NULL;

#define SINGLETONINSTANCE(T)                        \
    CSingleton< T >::Instance()

#define SINGLETON(T)                                \
    protected:                                      \
        friend class CSingleton< T >;               \
        T(T *) {}                                   \
        T(){}

#define SINGLETONCONSTRUCTOROVERRIDE(T)             \
    protected:                                      \
        friend class CSingleton< T >;               \
        T(T *) {}


#endif  // #ifndef SINGLETON_H
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700
