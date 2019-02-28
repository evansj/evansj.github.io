---
layout: post
title: Rails-like 'flash' in Spring
tags: []
typo_id: 316
---
I'm going to document this because it took me ages to work out, but in the end it turned out to be quite easy.

In [Rails](http://rubyonrails.org) there is a useful thing called ['flash'](http://api.rubyonrails.org/classes/ActionController/Flash.html). Flash is a component which is automatically available in every view. Controller classes can insert a message into the flash object, and when it renders the view it can display the message. The great thing is that by default the message exists in the flash for two requests. This is so that the current request can be terminated with a browser redirect, and when the browser follows the redirect the flash message will be there waiting for it.

[Read on]({{ site.baseurl }}{% post_url 2007-12-13-rails-like-flash-in-spring-part-1 %}) for more details.
