---
layout: post
title: "Jekyll로 블로그 만들기"
subtitle: "너도 나도 할 수 있는 블로그"
date: 2018-08-20 00:00:00
background: '/img/bg-post.jpg'
category: jekyll/blog
---

홈페이지를 만들기 위한 작업을 기록합니다.


https://bnhr.xyz/2017/03/25/add-syntax-highlighting-to-your-jekyll-site-with-rouge.html
 rougify style github > assets/syntax.scss


아무리 따라 해도안되는 현상
scss로 저장을 안해서
```
<link rel="stylesheet" href="{{"/assets/syntax.css" | relative_url }}>
```

build된 이후 처리가 되어야 하는데 그것이 안되니 문제
절대경로 css로 넣어주면 잘됨


rougify help style

```python
def function():
  print('Yes')
```

~~~javascript
function syntaxHighlight(code) {
   var foo = 'Hello World';
   var bar = 100;
}
~~~

{% highlight c++ %}

some code here

{% endhighlight %}


```yaml
 title: ruvieye's blog
 email: ruvieye@naver.com
 description: Continuous devlog
 author: ruvieye
 baseurl: ""
 url: "http://ruvieye.github.io"

 # Social Profiles
 twitter_username:  ruvieye
 github_username:   ruvieye
 facebook_username: ruvieye

 # Build settings
 markdown:          kramdown
 paginate:          7
 paginate_path:     "/posts/page:num/"
 plugins:
   - jekyll-feed
   - jekyll-paginate
   - jekyll-gist

```
{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}


{% gist c08ee0f2726fd0e3909d %}

