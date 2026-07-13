---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/visitor.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/base/visitor.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| struct | **[sgns::lambda_visitor< Lambda, Lambdas... >](/source-reference/Classes/d2/d5d/structsgns_1_1lambda__visitor_3_01_lambda_00_01_lambdas_8_8_8_01_4/)**  |
| struct | **[sgns::lambda_visitor< Lambda >](/source-reference/Classes/dc/d78/structsgns_1_1lambda__visitor_3_01_lambda_01_4/)**  |

## Functions

|                | Name           |
| -------------- | -------------- |
| template <class... Fs\> <br/>auto | **[make_visitor](/source-reference/Files/d2/df0/visitor_8hpp/#function-make_visitor)**(Fs &&... fs)<br/>Creates a compile-time visitor from a set of lambdas.  |
| template <typename TVariant ,typename... TVisitors\> <br/>decltype(auto) | **[visit_in_place](/source-reference/Files/d2/df0/visitor_8hpp/#function-visit_in_place)**(TVariant && variant, TVisitors &&... visitors)<br/>Applies an in-place visitor to a boost::variant.  |
| template <typename T ,typename Matcher \> <br/>decltype(auto) | **[match](/source-reference/Files/d2/df0/visitor_8hpp/#function-match)**(T && t, Matcher && m)<br/>apply Matcher to optional T  |
| template <typename T ,typename... Fs\> <br/>decltype(auto) | **[match_in_place](/source-reference/Files/d2/df0/visitor_8hpp/#function-match_in_place)**(T && t, Fs &&... fs)<br/>construct visitor from Fs and apply it to optional T  |


## Functions Documentation

### function make_visitor

```cpp
template <class... Fs>
auto make_visitor(
    Fs &&... fs
)
```

Creates a compile-time visitor from a set of lambdas. 

**Return**: Visitor instance that dispatches to the provided lambdas. 

Example: ```cpp

make_visitor([](int a){ return 1; },
             [](std::string b) { return 2; });
```

This is essentially the same as: ```cpp

struct visitor : public boost::static_visitor<int> {
  int operator()(int a) { return 1; }
  int operator()(std::string b) { return 2; }
};
```


### function visit_in_place

```cpp
template <typename TVariant ,
typename... TVisitors>
decltype(auto) visit_in_place(
    TVariant && variant,
    TVisitors &&... visitors
)
```

Applies an in-place visitor to a boost::variant. 

Example: ```cpp

boost::variant<int, std::string> value = "1234";

visit_in_place(value,
               [](int v) { std::cout << "(int)" << v; },
               [](std::string v) { std::cout << "(string)" << v; });
```


### function match

```cpp
template <typename T ,
typename Matcher >
decltype(auto) match(
    T && t,
    Matcher && m
)
```

apply Matcher to optional T 

### function match_in_place

```cpp
template <typename T ,
typename... Fs>
decltype(auto) match_in_place(
    T && t,
    Fs &&... fs
)
```

construct visitor from Fs and apply it to optional T 



## Source code

```cpp
#ifndef SUPERGENIUS_VISITOR_HPP
#define SUPERGENIUS_VISITOR_HPP

#include <type_traits>
#include <utility>

#include <boost/variant/apply_visitor.hpp>

namespace sgns
{
    template <typename... Lambdas> struct lambda_visitor;

    template <typename Lambda, typename... Lambdas>
    struct lambda_visitor<Lambda, Lambdas...> : public Lambda, public lambda_visitor<Lambdas...>
    {
        using Lambda::operator();
        using lambda_visitor<Lambdas...>::operator();

        lambda_visitor( Lambda lambda, Lambdas... lambdas ) : Lambda( lambda ), lambda_visitor<Lambdas...>( lambdas... )
        {
        }
    };

    template <typename Lambda> struct lambda_visitor<Lambda> : public Lambda
    {
        using Lambda::operator();

        lambda_visitor( Lambda lambda ) : Lambda( lambda )
        {
        }
    };

    template <class... Fs> constexpr auto make_visitor( Fs &&...fs )
    {
        using visitor_type = lambda_visitor<std::decay_t<Fs>...>;
        return visitor_type( std::forward<Fs>( fs )... );
    }

    template <typename TVariant, typename... TVisitors>
    constexpr decltype( auto ) visit_in_place( TVariant &&variant, TVisitors &&...visitors )
    {
        return boost::apply_visitor( make_visitor( std::forward<TVisitors>( visitors )... ),
                                     std::forward<TVariant>( variant ) );
    }

    template <typename T, typename Matcher> constexpr decltype( auto ) match( T &&t, Matcher &&m )
    {
        return std::forward<T>( t ) ? std::forward<Matcher>( m )( *std::forward<T>( t ) )
                                    : std::forward<Matcher>( m )();
    }

    template <typename T, typename... Fs> constexpr decltype( auto ) match_in_place( T &&t, Fs &&...fs )
    {
        return match( std::forward<T>( t ), make_visitor( std::forward<Fs>( fs )... ) );
    }
}

#endif
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700
