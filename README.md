cache-marshal-test
==================

This app shows that Rails cache data is not persisted correctly between 3.2 and 4.1. This happens with any cache store
(this example uses the built in file store).

Clone this repository and make sure you have the `tmp/cache` path:

    mkdir -p tmp/cache

Then from `master` branch (Rails 3.2) create an item in the cache that it a hash:


```
$ git checkout master
$ rails console
Loading development environment (Rails 3.2.21)
2.1.5 :001 > Rails.cache.write('my_key', {a:1})
 => true
2.1.5 :002 > Rails.cache.read('my_key')
 => {:a=>1}
2.1.5 :003 > exit
```

Now check out the Rails 4.1 branch and retrieve the item.

```
$ git checkout rails_4.1.8
$ rails console
Loading development environment (Rails 4.1.8)
2.1.5 :001 > Rails.cache.read('my_key')
 => "\x04\b{\x06:\x06ai\x06"
2.1.5 :002 > exit
```

Note that the item is a string, not a hash.
