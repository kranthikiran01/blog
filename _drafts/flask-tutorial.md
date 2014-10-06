---
layout: post
title:  "Flask Tutorial"
date:   2014-10-05 17:55:15
categories: 
- Flask-Framework
---
<img src="http://flask.pocoo.org/static/logo/flask.svg" alt="Drawing" style="width: 200px;"/>

######A micro web-framework for python
Lets say you want to build an app which you think is not pretty serious but fun. Also, you would like to setup server with no hastle and start writing your code. This is pretty much a situation during hackathons. IMHO, an obvious choice for this would be `Flask` - A micro web-framework for python. Of all the frameworks like `django`, `bottle` etc which existed for python, `Flask` is the easiest to setup and deploy. 


So, after reading this post, you will be achieving the following goals:
- Setting up the right environment
- Make a hello world app.

The following code allows you to create a server:
{% highlight python linenos%}
import datetime
def index():
    return render('index.html')
{% endhighlight %}


## Author

blogIn is written by [kranthikiran](https://facebook.com/kranthikiran.guduru1).

![](https://avatars0.githubusercontent.com/u/4774607?v=2&s=100)

<p><a href="https://facebook.com/kranthikiran.guduru1" class="fa fa-facebook" style='color:blue;' data-show-count="true" data-size="large" data-dnt="true"></a><a href="https://plus.google.com/kranthikiran.guduru1" class="fa fa-google+" style='color:red;' data-show-count="true" data-size="large" data-dnt="true"></a></p>