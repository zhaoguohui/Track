# Track

[![Pod Version](http://img.shields.io/cocoapods/v/Track.svg?style=flat)](http://cocoadocs.org/docsets/Track/)
[![Pod Platform](http://img.shields.io/cocoapods/p/Track.svg?style=flat)](http://cocoadocs.org/docsets/Track/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/maquannene/Track/blob/master/LICENSE)

Track is a thread safe cache write by Swift. Composed of DiskCache and MemoryCache which support LRU.

Thread safe implement  by `dispatch_semaphore_t lock` and `DISPATCH_QUEUE_CONCURRENT`.

Memory and Disk cache algorithms policy use `LRU` (Least Recently Used) implement by `linked list`. So it is fast and support eliminate least recently used object according count limit, cost limit and age limit.
 
## Use

**Base use**

Support Sync and Async Set, Get, RemoveObject, RemoveAll and Subscript.

```swift
let track = Cache.shareInstance

track.set(object: "object", forKey: "key")

track.object(forKey: "key")

track.removeObject(forKey: "key") { (cache, key, object) in }

track.removeAllObjects { (cache, key, object) in }
```

**Other use**

MemoryCache and DiskCache has feature of LRU, so they can eliminate least recently used object according `countLimit`, `costLimit` and `ageLimit`.

```swift
let diskcache = DiskCache.shareInstance

diskcache.countLimit = 20

diskcache.trimToAge(200)

let memorycache = MemoryCache.shareInstance

memorycache.trimToCost(1024 * 10)

memorycache.trimToCount(10) { (cache, key, object) in }
```

## Installation

```ruby
source 'https://github.com/CocoaPods/Specs.git'
platform :ios, '8.0'
use_frameworks!

pod 'Track'
```

If you want to use the latest features of Track

```
pod 'Track', :git => 'https://github.com/maquannene/Track.git'
```

## Thanks

Thanks YYCache，PINCache very much. Some ideas from them.

## License

Track is released under the MIT license.