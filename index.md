---
layout: page
---
{% include JB/setup %}

## Siyong Ma

Hi, I am Siyong Ma, and now a Master candidate in Computer Science program in Northeastern University, Boston, MA. I earned my Bachelor's degree of Engineering in Software Engineering from [East China Normal University](http://www.ecnu.edu.cn), July, 2013.

I am looking for 2014 summer research/industry internship and COOP intern opportunity for Spring 2015. I am a good learner, and eager to participate in information retrieval, machine learning and big data related research/work!

I am familiar with Python, Java, and C++. 

![Me](/image/me.jpg)

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>



