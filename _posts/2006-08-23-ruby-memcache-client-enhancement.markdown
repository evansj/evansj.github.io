---
layout: post
title: Ruby memcache-client enhancement
tags:
- Cache
- Ruby
typo_id: 122
---
Recently I have been refactoring some code so that various computed results are saved in a memcached cache to improve performance.

A common cache idiom is:

1. Compute cache key
2. look up key in cache
3. if value found, return it
4. else, run some code to generate the required value
5. save the generated value in the cache
6. return the value

It's quite awkward to have that code repeated all over your app, so I hit upon the idea
of passing a block to `Cache#get()` which would be used to compute
the value if the key wasn't found in the cache.

<!-- read more -->

My proof of concept code to add this functionality to the `Cache` module is:

```ruby
    module Cache
      class << self
        alias _get get
      end
  
      def self.get(key, expiry = 0)
        value = _get(key)
        if value.nil? && block_given?
          value = yield
          put(key, value, expiry)
        end
        value
      end
    end
```

If no block is given, it works exactly the same as the original get() method.  If a block is given then the block is
executed to generate the value if it isn't found in the cache.  The value is then stored in the cache and returned.

My code looks nicer now, instead of this:

```ruby
    cache_key = "#{some}/#{vars}"
    value = Cache.get cache_key
    unless value
      value = a_SOAP_call_that_takes_a_few_seconds()
      Cache.put cache_key, value, 10.minutes
    end
    value
```

I now have this:

```ruby
    Cache.get("#{some}/#{vars}", 10.minutes) do
      a_SOAP_call_that_takes_a_few_seconds()
    end
```

I have [logged this possible enhancement][bug] to the bug tracker for memcache-client.

[bug]: https://web.archive.org/web/20080128071219/http://rubyforge.org/tracker/index.php?func=detail&aid=5495&group_id=1266&atid=4981 "[#5495] [ENHANCEMENT] Better implementation of Cache.get"
