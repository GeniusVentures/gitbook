---
title: /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/watcher/messaging_watcher.hpp

---

# /Users/Shared/SSDevelopment/Development/GeniusVentures/GeniusNetwork/SuperGenius/src/watcher/messaging_watcher.hpp





## Namespaces

| Name           |
| -------------- |
| **[sgns](/source-reference/Namespaces/d2/d2b/namespacesgns/)**  |
| **[sgns::watcher](/source-reference/Namespaces/d4/d7f/namespacesgns_1_1watcher/)**  |

## Classes

|                | Name           |
| -------------- | -------------- |
| class | **[sgns::watcher::MessagingWatcher](/source-reference/Classes/d9/deb/classsgns_1_1watcher_1_1_messaging_watcher/)**  |




## Source code

```cpp
#ifndef MESSAGING_WATCHER_HPP
#define MESSAGING_WATCHER_HPP

#include <functional>
#include <string>
#include <boost/thread.hpp>
#include <rapidjson/document.h>

namespace sgns::watcher {

    class MessagingWatcher
    {
    public:
        using MessageCallback = std::function<void(const std::string &)>;

        virtual ~MessagingWatcher() = default;

        virtual void startWatching();
        virtual void stopWatching();

        bool isRunning() const;

        // Static methods to manage all watchers
        static void addWatcher(const std::shared_ptr<MessagingWatcher> &newWatcher);
        static void startAll();
        static void stopAll();

    protected:
        // Protected callback to be used by derived classes
        MessageCallback messageCallback;
        // Constructor that takes a callback to initialize messageCallback
        explicit MessagingWatcher(MessageCallback callback);

        bool running;
        mutable std::mutex running_mutex;
        boost::thread watcherThread;

        // Protected virtual watch function to be overridden by derived classes
        virtual void watch();

    private:
        // Static vector to hold all watcher instances
        static std::vector<std::shared_ptr<MessagingWatcher>> m_watchers;
    };

}  // namespace sgns::watcher

#endif // MESSAGING_WATCHER_HPP
```


-------------------------------

Updated on 2026-07-09 at 16:47:34 -0700
