---
layout: post
title: "Hello Jack"
description: ""
category: haskell
tags: []
---
* For a file on disk, you can use sendFile in your handler.
{% highlight haskell %}
getImageR = do
    -- ... save image data to disk somewhere
    sendFile typeJpeg "/path/to/file.jpg"
{% endhighlight %}
* For sending it from a ByteString in memory, use sendResponse.
{% highlight haskell %}
getImageR = do
    bytes <- -- generate image data
    sendResponse (typePng, toContent bytes)
{% endhighlight %}
* [Haskell官网](http://www.haskell.org/haskellwiki/Haskell)
* 更新命令 
{% highlight bash %}
git add -u
git commit -m "new content"
git push origin master
{% endhighlight %}
{% include references.md %}
