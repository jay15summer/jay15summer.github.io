---
layout: defaults/page
permalink: index.html
narrow: true
---

{% include components/intro.md %}

[More about me]({{ site.baseurl}}{% link _pages/about.md %})

### What's in my site?
I am posting interesting problems and useful techniques that appear in my Ph.D. study. The [posts](https://jay15summer.github.io/list/posts.html) in this site are mostly with the following topics:

* Regression/classification
* Spatial statistics
* Transfer learning
* Useful Python/R/Matlab packages/techniques

Also, I will post some of my [research projects](https://jay15summer.github.io/list/projects.html) which use data modeling and machine learning methods to deal with manufacturing process quality control and diagnosis, e.g., engine deck surface variation modeling, surface assembly modeling.

### Recent Posts
{% for post in site.posts limit:4 %}
{% include components/post-card.html %}
{% endfor %}

<div class="d-flex align-items-center mt-2">
<a>Lastly, a beautiful picture!</a>
    <span class="icon grey mr-1">
        {% include entypo/arrow-down.svg %}
    </span>
</div>

<div class="card mb-3">
    <img class="card-img-top" src="https://raw.githubusercontent.com/jay15summer/jay15summer.github.io/master/assets/images/image1_twilight.jpg"/>
    <div class="card-body bg-light">
        <div class="card-text">Twilight at CoE FSU.</div>
    </div>
</div>
