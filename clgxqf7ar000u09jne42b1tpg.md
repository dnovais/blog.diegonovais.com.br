---
title: "Fixing the error: can't find gem bundler"
datePublished: Wed Apr 26 2023 13:28:46 GMT+0000 (Coordinated Universal Time)
cuid: clgxqf7ar000u09jne42b1tpg
slug: fixing-the-error-cant-find-gem-bundler
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/5b6AfmGN9AE/upload/2abcd07336347ace889436f74d23c4d1.jpeg
tags: ruby-on-rails, bundler, error-fixing

---

Greetings friends!

If you are in a rails project and need to install the gem `bundler`, but you got this error:

```bash
can't find gem bundler (>= 0.a)
```

The best way to install the gem bundler and avoid or fix this error is to install the bundler gem by getting the specific version contained in the `Gemfile.lock` with the command below:

```bash
gem install bundler -v "$(grep -A 1 "BUNDLED WITH" Gemfile.lock | tail -n 1)"
```

I hope that this content helps you! See you in the next article!