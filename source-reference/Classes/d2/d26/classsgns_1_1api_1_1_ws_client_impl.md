---
title: sgns::api::WsClientImpl

---

# sgns::api::WsClientImpl






`#include <ws_client_impl.hpp>`

Inherits from std::enable_shared_from_this< WsClientImpl >

## Public Types

|                | Name           |
| -------------- | -------------- |
| using boost::asio::io_context | **[Context](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#using-context)**  |
| using boost::asio::strand< boost::asio::io_context::executor_type > | **[ExecutorType](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#using-executortype)**  |
| using boost::asio::basic_stream_socket< boost::asio::ip::tcp > | **[StreamSocket](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#using-streamsocket)**  |
| using boost::beast::websocket::stream< [StreamSocket](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#using-streamsocket) > | **[PlainWebSocketStream](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#using-plainwebsocketstream)**  |
| using boost::beast::ssl_stream< [StreamSocket](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#using-streamsocket) > | **[SSLStream](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#using-sslstream)**  |
| using boost::beast::websocket::stream< [SSLStream](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#using-sslstream) > | **[SecureWebSocketStream](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#using-securewebsocketstream)**  |

## Public Functions

|                | Name           |
| -------------- | -------------- |
| | **[WsClientImpl](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#function-wsclientimpl)**([Context](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#using-context) & context, const std::string & url) |
| void | **[start](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#function-start)**() |
| void | **[setMessageHandler](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#function-setmessagehandler)**(std::function< void(const std::string &)> handler) |
| void | **[send](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#function-send)**(const std::string & message) |
| void | **[stop](/source-reference/Classes/d2/d26/classsgns_1_1api_1_1_ws_client_impl/#function-stop)**() |

## Public Types Documentation

### using Context

```cpp
using sgns::api::WsClientImpl::Context = boost::asio::io_context;
```


### using ExecutorType

```cpp
using sgns::api::WsClientImpl::ExecutorType = boost::asio::strand<boost::asio::io_context::executor_type>;
```


### using StreamSocket

```cpp
using sgns::api::WsClientImpl::StreamSocket = boost::asio::basic_stream_socket<boost::asio::ip::tcp>;
```


### using PlainWebSocketStream

```cpp
using sgns::api::WsClientImpl::PlainWebSocketStream = boost::beast::websocket::stream<StreamSocket>;
```


### using SSLStream

```cpp
using sgns::api::WsClientImpl::SSLStream = boost::beast::ssl_stream<StreamSocket>;
```


### using SecureWebSocketStream

```cpp
using sgns::api::WsClientImpl::SecureWebSocketStream = boost::beast::websocket::stream<SSLStream>;
```


## Public Functions Documentation

### function WsClientImpl

```cpp
WsClientImpl(
    Context & context,
    const std::string & url
)
```


### function start

```cpp
void start()
```


### function setMessageHandler

```cpp
void setMessageHandler(
    std::function< void(const std::string &)> handler
)
```


### function send

```cpp
void send(
    const std::string & message
)
```


### function stop

```cpp
void stop()
```


-------------------------------

Updated on 2026-07-09 at 16:47:33 -0700