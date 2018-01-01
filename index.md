---
# You don't need to edit this file, it's empty on purpose.
# Edit theme's home layout instead if you wanna make some changes
# See: https://jekyllrb.com/docs/themes/#overriding-theme-defaults
layout: home
---

Welcome to codewithnate.com! This companion blog
to [Code With Nate YouTube Channel](https://www.youtube.com/channel/UCPrcrJwwcMGWpOv_qRJOuIA)
is designed to teach web programming concepts in small, digestible chunks.

I'm Nate Turner, producer of Code With Nate. I'm passionate about using the enormous
amount of freely available software components to build useful web services, websites
and tools. Leveraging freely available software, diligent programmers can make their lives,
and the lives of their users better.

This site is made for anybody interested in topics hosted on either this blog,
or the [YouTube Channel](https://www.youtube.com/channel/UCPrcrJwwcMGWpOv_qRJOuIA). Posts range
from beginner to advanced levels on a large variety of topics including full stack development,
deployment, security ops and more.

Viewers can request new content at the
[YouTube Channel Discussion Page](https://www.youtube.com/channel/UCPrcrJwwcMGWpOv_qRJOuIA/discussion).
So far, every request has resulted in a new video!

{% for post in site.posts %}
    <h3><a href="{{ post.url }}">{{ post.title }}</a></h3>
    <p><small><strong>{{ post.date | date: "%B %e, %Y" }}</strong> . {{ post.category }} . <a href="http://erjjones.github.com{{ post.url }}#disqus_thread"></a></small></p>
{% endfor %}