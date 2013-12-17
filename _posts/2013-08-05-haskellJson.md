---
layout: post
title: "haskell json 操作"
description: ""
category: haskell
tags: [haskell,yesod]
---
{% highlight haskell %}
* 从string to lazy bytestring

  let t =Data.ByteString.Lazy.UTF8.fromString jsonstr


* 从lazystring to Maybe Map

let a=Data.Aeson.decode t :: Maybe (Map String Object)


* Map 查询

Data.Map lookup "result" (fromJust a)

{% endhighlight %}


{% include references.md %}
