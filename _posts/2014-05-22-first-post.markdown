---
layout: post
title:  "First Post"
categories: blog coding
tags: jekyll practice 1
---

Yeepee - first post! Welcome!

This is intended to be a blog that I will use to express my musings, thoughts, and other things that pop into my head - possibly computer related. Possibly not. Probably yes, though.

A bit about myself - my name is Ben, and I just graduated from McGill University in frosty Montreal. Since I've majored in Computer Science (and Economics, but who really cares about that?), I figured I should use a bit of my spare time to create a nice little programming-related blog, like every good software developer should do.

A good place to start is to probably describe how I built this blog. I built it using [Jekyll][jekyll], a static-site generator created by the wonderful people at [Github] [github] (well, [mostly wonderful][github_trouble]). 

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll's GitHub repo][jekyll-gh].	

[jekyll]:    http://jekyllrb.com
[github]:    http://jekyllrb.com
[github_trouble]:    http://techcrunch.com/2014/03/15/julie-ann-horvath-describes-sexism-and-intimidation-behind-her-github-exit/

{{ page.tags }}