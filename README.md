# go-cache
Implements a generic cache in Golang (1.18)

# Installation

```sh
go get github.com/AlexandreChamard/go-cache
```

# Examples

```golang
import (
    "time"

    "github.com/AlexandreChamard/go-cache"
)

/*
options := NewCacheOptions().
    CacheDuration(time.Duration). // Default duration given for each item insert with Set
    NoExpiration(). // No expiration by default
    MaxSize(int). // set the max item in the cache at the same time (automatically partially flush it when full)
    NoSizeLimit(). // No size limit by default
    CacheOffset(int). // Cache offset is mandatory when MaxSize is set but ignored if not (Default: 10% of the MaxSize)
    DefaultCacheOffset(). // Set the default cacheOffset (ony used if MaxSize is defined)
    PurgeTimer(time.Duration). // Calls DeleteExpiredItems at every duration given (Default: 1 minute)
    NoPurge() // You have to call DeleteExpiredItems by hands
*/

cache := cache.NewCache[int, int](NewCacheOptions().CacheDuration(30 * time.Second))

cache.Set(0, 42)
cache.Set(1, 30)
cache.SetWithExpiration(2, 69, time.Hour) // Override the default cacheDuration

time.Sleep(2*time.Minute) // wait 2 time the purge timer to be sure it happens

_, ok := cache.Get(0) // ok == false
_, ok = cache.Get(1)  // ok == false
k, ok := cache.Get(2)  // ok == true ; k = 69
```
