---
layout: default
title: JavaScript API
---

# Seldon JavaScript API

The Seldon JavaScript API provides the simplest method of integrating Seldon onto web based services. It provides two methods:

* User Action : Called from each web page where a user performs an action, e.g. loads the web page on a news site.
* User Recommendation : Called to get recommedations for the current user to display on the page, e.g. to fill a recommendations box on a news web site with articles the user may be interested in reading. 

For details on the overall concepts of users, items and actions see the [Oauth API](api-oauth.html)

## Self contained JS Library
Seldon has a self contained drop in library which contains these calls which it will be releasing soon.

## User Action

{% highlight http %}
GET     /js/actions
{% endhighlight %}

Input

* consumer_key 
* user : user id of current user 
* item : currently viewed item id
* type : type of action
* jsonpCallback : jsonp callback

Example

{% highlight http %}
http://<HOST>/js/action/new?consumer_key=XYZ&user=1&item=2&type=1&jsonpCallback=j
{% endhighlight %}


{% highlight json %}
{
	"actionId":null,
	"user":"1",
	"item":"2",
	"type":1,
	"date":1421336333669,
	"value":0.0,
	"times":1,
	"comment":null,
	"tags":null,
	"recTag":null,
	"referrer":null
}
{% endhighlight %}	

## User Recommendations

{% highlight http %}
GET     /js/recommendations
{% endhighlight %}

Input

* consumer_key 
* user : user id of current user 
* item : currently viewed item id
* limit :  max recommended items to return
* dimension : dimension to use (e.g., just sports articles) 
* attributes : fields to return for each recommended item
* algorithms : override the default algorithms with specific ones
* jsonpCallback : jsonp callback

Example

{% highlight http %}
http://<HOST>/js/recommendations?consumer_key=XYZ&user=1&limit=3&attributes=title&jsonpCallback=j
{% endhighlight %}

{% highlight json %}
j({
	"size":3,
	"requested":3,
	"list":[
		{
		"id":"500",
		"name":"Mrs. Doubtfire (1993)",
		"type":1,
		"first_action":1421080898000,
		"last_action":1421080898000,
		"demographics":[],"attributes":{"12":616,"1":1,"11":582},
		"attributesName":{"title":"Mrs. Doubtfire (1993)","recommendationUuid":"3"}},
		{"id":"586",
		"name":"Home Alone (1990)",
		"type":1,
		"first_action":1421080898000,
		"last_action":1421080898000,
		"demographics":[],
		"attributes":{"12":542,"1":1,"11":541},
		"attributesName":{"title":"Home Alone (1990)","recommendationUuid":"3"}},
		{"id":"153",
		"name":"Batman Forever (1995)",
		"type":1,
		"first_action":1421080898000,
		"last_action":1421080898000,
		"demographics":[],
		"attributes":{"1":1,"11":1,"12":2,"13":35,"14":36},
		"attributesName":{"title":"Batman Forever (1995)","recommendationUuid":"3"}}
		]
})
{% endhighlight %}	

