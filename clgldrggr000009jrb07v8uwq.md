---
title: "Installing lower version of Ruby using ASDF"
seoTitle: "Installing lower version of Ruby using ASDF"
seoDescription: "Installing lower version of Ruby using ASDF"
datePublished: Mon Apr 17 2023 22:01:09 GMT+0000 (Coordinated Universal Time)
cuid: clgldrggr000009jrb07v8uwq
slug: installing-lower-version-of-ruby-using-asdf
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/VKLJ-BJlszE/upload/ff884b51ca7c75ad6f3c83b23b5963e5.jpeg
tags: ruby, tips-and-tricks, developer, installation

---

Greetings! The other day, I was having trouble installing a lower version of **Ruby** using `ASDF` and after trying to solve around a bit, I figured out a solution. This solution might not work for everyone, but I wanted to share it in case it helps.  
  
If you need to install a lower version of **Ruby** using `ASDF` and you are using a **Mac OS** and a chip **M1**:

```bash
asdf install ruby 2.5.6
```

and get this error:

```bash
Downloading openssl-1.1.1q.tar.gz...
-> https://dqw8nmjcqpjn7.cloudfront.net/d7939ce614029cdff0b6c20f0e2e5703158a489a72b2507b8bd51bf8c8fd10ca
Installing openssl-1.1.1q...
patching file 'test/v3ext.c'
Installed openssl-1.1.1q to /Users/diegonovais/.asdf/installs/ruby/2.5.6

Downloading ruby-2.5.6.tar.gz...
-> https://cache.ruby-lang.org/pub/ruby/2.5/ruby-2.5.6.tar.gz
Installing ruby-2.5.6...

WARNING: ruby-2.5.6 is past its end of life and is now unsupported.
It no longer receives bug fixes or critical security updates.

ruby-build: using readline from homebrew

BUILD FAILED (macOS 13.1 using ruby-build 20220910.1)

Inspect or clean up the working tree at /var/folders/tz/30dwng7x0yj3wx155zn208rh0000gn/T/ruby-build.20230417122109.83173.Iy6xtk
Results logged to /var/folders/tz/30dwng7x0yj3wx155zn208rh0000gn/T/ruby-build.20230417122109.83173.log

Last 10 log lines:
compiling ../.././ext/psych/yaml/emitter.c
compiling ../.././ext/psych/yaml/parser.c
5 warnings generated.
26 warnings generated.
linking shared-object zlib.bundle
1 warning generated.
linking shared-object psych.bundle
436 warnings generated.
linking shared-object date_core.bundle
make: *** [build-ext] Error 2
```

**To fix it**, you need to run the following command:

```bash
RUBY_CFLAGS="-w" asdf install ruby 2.5.6
```

I hope that this content helps you! See you in the next article!