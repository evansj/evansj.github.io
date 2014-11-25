---
layout: post
title: Fix Ruby on Mac OS X 10.4
tags:
- Ruby
- OSX
- Rails
typo_id: 115
---
Mac OS X 10.4 comes with [ruby](http://ruby-lang.org/) 1.8.2, it seems to have a problem with [OpenSSL](http://www.openssl.org/) which causes [`switchtower`](http://manuals.rubyonrails.com/read/book/17) to [hang](http://jamis.jamisbuck.org/articles/2005/09/24/switchtower-on-osx) when trying to connect to your server.

You can download the source code to Ruby 1.8.3, compile it and install it, but you'll start getting weird errors in `gem` when you try to install some libraries.

The solution turned out to be to compile Ruby slightly differently.  You need to pass some flags to configure:

    ./configure --enable-shared --enable-pthread

After configuring it, `make`ing it, and running `sudo make install`, I had what seemed to be a working Ruby installation.  It installs to `/usr/local/bin` which is already in my path.  Executing `hash -r` causes `bash` to re-scan the path, after which executing `ruby -v` correctly reports

    ruby 1.8.3 (2005-09-21) [powerpc-darwin8.3.0]

After that I installed [RubyGems-0.8.11](http://rubyforge.org/projects/rubygems/) and the `rails` and `switchtower` gems, including all dependencies.  The installation worked fine, and so did `switchtower` when I tested it.

I didn't even need to remove Apple's Ruby install.

If you do want to remove Apple's installation of Ruby, you'll want to back up and delete the following files and directories:

    /usr/bin/erb
    /usr/bin/irb
    /usr/bin/rdoc
    /usr/bin/ri
    /usr/bin/ruby
    /usr/bin/testrb
    /usr/bin/gem
    /usr/bin/gem_server
    /usr/bin/gemwhich
    /usr/bin/rake
    
    /usr/lib/ruby/
    /usr/lib/libruby.1.dylib
    /usr/lib/libruby.dylib
    
    /usr/share/ri/
