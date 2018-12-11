---
title:  "How To: Blog With Jekyll"
categories: jekyll howto
---

Open GitBash. Check whether you have Ruby installed in your machine or not.

{% highlight git %}
ruby -v
{% endhighlight %}

If it's not there you can download and install Ruby from here https://rubyinstaller.org/.

Install all three options 1, 2, 3 respectively.

{% highlight git %}
gem -v
{% endhighlight %}

Install jekyll bundler using gem.

{% highlight git %}
gem install jekyll bundler
{% endhighlight %}

Create a blog using jekyll. it's a scaffolder to generate all necessary files with structures.

{% highlight git %}
jekyll new blog_name
{% endhighlight %}

Go inside blog_name and execute following code.

{% highlight git %}
bundle exec jekyll serve
{% endhighlight %}

Please note that budle exec you'll only need the first time. From here on
after changing anythin to your site, you can only execute jekyll serve,
it'll publish all your changes to server.

It'll fire up your blog in http://localhost:4000/

You're ready to publish!

{% highlight git %}
git add -all
git commit -m 'Hello, World!'
git push
{% endhighlight %}

Browse to https://UserName.github.io

Voila! You have your own blog published to the world.

Happy Blogging!

1) [Github Official Page](https://pages.github.com/)
2) [Tutorial](https://www.youtube.com/watch?v=T1itpPvFWHI&list=PLLAZ4kZ9dFpOPV5C5Ay0pHaa0RJFhcmcB)
