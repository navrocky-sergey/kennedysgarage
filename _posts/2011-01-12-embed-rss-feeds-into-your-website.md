---
layout: article
permalink: /articles/embed-rss-feeds-into-your-website
title: Embed RSS Feeds into your website
excerpt: After hours of looking for a simple &amp; reliable way to post Atom, RSS, or Media RSS feeds on a website I have finally found a solution. Today we will be going over Google Feed API and how to set it up on your site. I also want to make a note that it is
---

<p>After hours of looking for a simple &amp; reliable way to post Atom, RSS, or Media RSS feeds on a website I have finally found a solution. Today we will be going over <a href="http://code.google.com/apis/feed/">Google Feed API</a> and how to set it up on your site. I also want to make a note that it is also real easy to customize the look and feel with CSS with this script. Here is the final code:</p>

{% highlight javascript %}
&lt;script src=&quot;http://www.google.com/jsapi?key=YOURAPIKEY&quot; type=&quot;text/javascript&quot;&gt;&lt;/script&gt;
&lt;script type=&quot;text/javascript&quot;&gt;
    google.load(&quot;feeds&quot;, &quot;1&quot;);
    function OnLoad() {
    var feedControl = new google.feeds.FeedControl();
    feedControl.addFeed(&quot;http://news.google.com/news?pz=1&amp;cf=all&amp;ned=us&amp;hl=en&amp;output=rss&quot;);
    feedControl.draw(document.getElementById(&quot;google-news&quot;));
    }
    google.setOnLoadCallback(OnLoad);
&lt;/script&gt;

&lt;div id=&quot;google-news&quot;&gt;Loading...&lt;/div&gt;
{% endhighlight %}

<p>Lets brake it down so we have a better understanding what each part is and then we will talk about the extras.</p>

<h3>Google API Key</h3>
{% highlight html %}
&lt;script src=&quot;http://www.google.com/jsapi?key=YOURAPIKEY&quot; type=&quot;text/javascript&quot;&gt;&lt;/script&gt;
{% endhighlight %}

<p>This first part is basically calling all libraries that we might need for whatever application that we build. It also includes your API Key which just adds more data to that script. It has some other uses that are not necessary to worry about with just this script. Now go ahead and <a href="http://code.google.com/apis/loader/signup.html">sign up for an API key</a>. You are going to replace "YOURAPIKEY" with the newly generated key in the script.</p>

<h2>The Meat</h2>
<p>The next part is the meat of it. This is where we can get down to the details and tell Google what we want.</p>

<h3>Load Request</h3>
{% highlight html %}
google.load(&quot;feeds&quot;, &quot;1&quot;);
{% endhighlight %}

<p>The load request tells Google what type of API we are building. Today we are going to be building with the Google Feed API. The 1 represents the version number. As of today there is only one version. </p>

<h3>onLoad</h3>
{% highlight javascript %}
function OnLoad()
{% endhighlight %}

<p>The onLoad event handler is used to call the execution of JavaScript after the page has completely loaded. Basically it will run the script after the page is loaded.</p>

<h3> Create a feed control</h3>
{% highlight javascript %}
var feedControl = new google.feeds.FeedControl();
{% endhighlight %}

<p>Now you will simply declare the variable.</p>

<h3>Add the feed</h3>
{% highlight javascript %}
feedControl.addFeed(&quot;http://news.google.com/news?pz=1&amp;cf=all&amp;ned=us&amp;hl=en&amp;output=rss&quot;);
{% endhighlight %}

<p>This is where you are going to specify the URL of the feed. For this example I am using <a href="http://news.google.com">Google News</a>.</p>

<h3>Draw it</h3>
{% highlight javascript %}
feedControl.draw(document.getElementById(&quot;google-news&quot;));
{% endhighlight %}

<p>This is telling the script where to put the information that it is receiving. In this example I named my ID "google-news". In a bit you will see the second half of this part.</p>

<h3>Callback</h3>
{% highlight javascript %}
google.setOnLoadCallback(OnLoad);
{% endhighlight %}

<p>I am not 100% sure about this part does, but from what I understand it is specific handler function to be called once the document loads. I think this has to something to do when dealing with more then one or search functions. Please let me know if you have the correct answer.</p>

<h3>The HTML</h3>
{% highlight javascript %}
&lt;div id=&quot;google-news&quot;&gt;Loading...&lt;/div&gt;
{% endhighlight %}

<p>This is in reference to a JavaScript part titled "Draw it". It is more or less the place holder for where the script will load the content into. As I said before I have named my ID "google-news". Feel free to change this to whatever you want as long as you remember to change it in the Javascript.</p>


<h2>The Extra</h2>

<h3>Set number of post</h3>
{% highlight javascript %}
feedControl.setNumEntries(11);
{% endhighlight %}

<p>By default Google is preset to show 4 post. This can be easily changed by adding that bit of code to the JavaScript as such.</p>

{% highlight javascript %}
&lt;script type=&quot;text/javascript&quot;&gt;
google.load(&quot;feeds&quot;, &quot;1&quot;);
function OnLoad() {
var feedControl = new google.feeds.FeedControl();
feedControl.addFeed(&quot;http://news.google.com/news?pz=1&amp;cf=all&amp;ned=us&amp;hl=en&amp;output=rss&quot;);
feedControl.setNumEntries(11);
feedControl.draw(document.getElementById(&quot;google-news&quot;));
}
google.setOnLoadCallback(OnLoad);
&lt;/script&gt;
{% endhighlight %}

<h3>Set multiple feeds &amp; add a title</h3>
{% highlight javascript %}
&lt;script type=&quot;text/javascript&quot;&gt;
google.load(&quot;feeds&quot;, &quot;1&quot;);
function OnLoad() {
    var feedControl = new google.feeds.FeedControl();
    feedControl.addFeed(&quot;http://news.google.com/news?pz=1&amp;cf=all&amp;ned=us&amp;hl=en&amp;output=rss&quot;, &quot;Google News&quot;);
    feedControl.addFeed(&quot;http://kennedysgarage.com/feed/rss/&quot;, &quot;Kennedy&#39;s Garage&quot;);
    feedControl.draw(document.getElementById(&quot;google-news&quot;));
}
google.setOnLoadCallback(OnLoad);
&lt;/script&gt;
{% endhighlight %}

<p>So far I have only showed you how to draw in one RSS feed. With this script you can draw as many as you would like on the same page. You can also give then titles so you don't mix them up.</p>

<h2>Thats it</h2>
<p>I hope you have learned how not to beat your head into your desk. If you have any questions please feel free to ask. Also if you have any other ideas on how to modify the feed please let me know. </p>

<h2>Source</h2>
<p>
<a href="http://code.google.com/apis/ajax/playground/?exp=newssearch#feed_control">Google Code Playground</a><br/>
<a href="http://code.google.com/apis/feed/v1/reference.html">Google Feed API Documentation </a>
</p>