---
title:  "How To: Create GitHub Page"
categories: githubpage howto
---

Head over to GitHub and create a new repository named username.github.io,
where username is your username (or organization name) on GitHub.

If the first part of the repository doesn’t exactly match your username,
it won’t work, so make sure to get it right.

![image tooltip here](/img/new_repo.png)

Go to github homepage. You'll see all your repositories listed there.
Click on your repository.

![image tooltip here](/img/repo_list.png)

This is your repository home page. Copy the link of repository to clone.

![image tooltip here](/img/clone_repo.png)

Open GitBash. Clone your repository. It'll create a folder with your repository
name.

{% highlight git %}
git clone https://github.com/UserName/UserName.github.io.git
{% endhighlight %}

Create a html file.

{% highlight git %}
git add -all
{% endhighlight %}

{% highlight git %}
git commit -m 'Hello, World!'
{% endhighlight %}

{% highlight git %}
git push
{% endhighlight %}

Browse [here](https://UserName.github.io) to view your site.

Voila! You have your own site.
