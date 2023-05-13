---
title: "Setting the version of a Gem on Gemfile"
datePublished: Tue May 09 2023 03:21:17 GMT+0000 (Coordinated Universal Time)
cuid: clhfpg1qo000109jzfyoqgpow
slug: setting-the-version-of-a-gem-on-gemfile
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/qayNP9ccw9E/upload/88561eaa88f2511d5324c4006cc60536.jpeg
tags: software-development, ruby, ruby-on-rails, dependency-management, gemfile

---

Greetings Rubysts,

Setting the version of a Gem in the Gemfile is an essential step in managing dependencies for a Ruby project. The Gemfile allows you to specify the version of a Gem that your project requires, ensuring that all project contributors are using the same version of the Gem and minimizing the risk of compatibility issues. This can be especially important if your project relies on multiple Gems or if you are working on a large team. Additionally, specifying the version of a Gem in the Gemfile can help ensure that your project remains stable and secure by allowing you to control when and how updates to the Gem are applied. Below are some examples of how to do this:

1. **Use a specific version:**
    

```ruby
gem 'example_gem', '1.2.3'
```

In this example, we set the specific version `1.2.3` of the Gem `example_gem`.

1. **Setting only a range of compatible versions of the Gem:**
    

```ruby
gem 'example_gem', '~> 1.2.0'
```

The example provided means that any version of the gem `example_gem` starting with 1.2 up to, but not including the major update is compatible with the project. So the range of compatible versions will be accepted, and it is the same as say that the gem `example_gem` will install only versions `>= 1.2.0` and `< 1.3.0`.

1. **Setting an interval between the accepted versions of the Gem:**
    

```ruby
gem 'example_gem', '>= 1.2.0', '< 1.3.0'
```

In this example, only the versions greater than `1.2.0` and less than `1.3.0` will be accepted.

1. **Setting the last version of the gem:**
    

```ruby
gem 'example_gem'
```

In this case, the most recent version of the gem will be installed.

1. **Setting a custom repository and branch for the gem:**
    

```ruby
gem 'example_gem', git: 'https://github.com/user/example_gem.git', branch: 'master'
```

Here the gem `example_gem` will be installed from a custom repository on Github and its branch.

1. **Setting a local path for the gem:**
    

```ruby
gem 'example_gem', path: '/path/to/exam_gem'
```

In some cases, it may be necessary or useful to install a Gem from a local path instead of from a remote source such as [rubygems.org](http://rubygems.org). This can be helpful for development and testing purposes, for example, when you are working on a Gem locally and want to test it in another project without publishing it to a remote repository. In this case, the Gemfile includes the gem example\_gem with the path to the local directory where the Gem is stored. This approach can help streamline development and testing processes and ensure that the Gem is being used consistently across projects.

I hope that this content was useful for you! See you in the next article!