Title: July is the month of buses, and 2016 is the year of JS
Date: 2016-07-22 08:32
Category: General
Tags: code
Slug: busroutejs

Yesterday, there I was, minding my own business, when Facebook 
"memories" or whatever threw this curveball at me:

![Bus Route Anniversary]({filename}/images/bus-route-anni.png)

Turns out it was exactly 5 years ago that I hacked together 
[a small piece of PHP][1], with a *liberal* amount of SQL logic 
thrown in, and it became sort of popular. We're talking a 
[codebase][2] like this:

```php
<?php 

function find3Bus($from, $to)
{
    global $dbconn;
    $sql = <<<SQL
SELECT s1.`bid` as busid1, s3.`bid` as busid2, s5.`bid` as busid3, 
ch1.`changeid` as changeid1, ch2.`changeid` as changeid2, 
(s2.`stopNo` - s1.`stopNo`) as dist1, 
(s4.`stopNo` - s3.`stopNo`) as dist2, 
(s6.`stopNo` - s5.`stopNo`) as dist3
FROM `changeover` AS ch1, `changeover` AS ch2, `stop` AS s1 INNER JOIN `stop` AS s2
ON s1.`bid` = s2.`bid`
INNER JOIN `stop` AS s3
ON s2.`pid` = s3.`pid`
INNER JOIN `stop` AS s4
ON s3.`bid` = s4.`bid`
INNER JOIN `stop` AS s5
ON s4.`pid` = s5.`pid`
INNER JOIN `stop` AS s6
ON s5.`bid` = s6.`bid`  
WHERE s1.`pid` = :from AND s2.`pid` = ch1.`changeid` AND s4.`pid` = ch2.`changeid` 
AND s6.`pid` = :to AND s2.`stopNo` > s1.`stopNo` AND s4.`stopNo` > s3.`stopNo` 
AND s6.`stopNo` > s5.`stopNo` ORDER BY (dist1 + dist2 + dist3);
SQL;
    $res    = $dbconn->query($sql, array(':from' => $from, ':to' => $to));
    $return = false;
    if($res && ($row = $res->fetch()) != false)
    {
        $return = $row;
    }
    return $return;
}

?>
```

Yikes.

Anyway, this was hosted on a shitty [000a host][3] that somehow 
still exists on the internet, and it looked like this:

![Bus Route Site Screenshot]({filename}/images/bus-route-original.png)

And gave out results that looked like:

![Bus Route Site Results]({filename}/images/bus-route-original-results.png)

Which somehow is better looking than anything I've managed since.

ANYWAY
------

I've been wanting to rewrite [this thing in JS since 2014][4], 
and I've been grappling with Dijkstra's algorithm for months 
over this. The moment of clarity was realising that bus routes 
*aren't graphs, they're linked lists*, and using complicated 
graph algorithms is unnecessary.

This Facebook reminder yesterday and having a *bit* of free
time on my hands led to a 24-hour code sprint that produced
[this little thingy][5].

It's not *better* than the original, for example the same query
as the above Galle Face - Kottawa one gives a stupid result 
like this:

![Bus Route JS Results]({filename}/images/bus-route-js-results.png)

The data is ~ 5 years old and needs to be tweaked, and I think 
the algorithms can do with a lot of tweaking, but here it is 
and it runs 100% client-side. Yay 2016!

What is this CRAP?!
-------------------

*Update:* The UI code is now completely React-based! All clean and 
beautiful. Yay!

"Janith", I hear you say, "you go around the place talking about 
the how great React is and how important readable code is, and 
then you write crap UI code like this:"

```javascript
if(route.changes.length == 0) {
    output = '<div class="col-xs-12">' + 
        renderRoute(route.from, route.to, route.distance, route.routes[0].routes) + '</div>';
}
else if(route.changes.length == 1) {
    output = '<div class="col-xs-6">' + 
        renderRoute(route.from, route.changes[0], route.routes[0].distance, route.routes[0].routes) + 
    '</div><div class="col-xs-6">' +
        renderRoute(route.changes[0], route.to, route.routes[1].distance, route.routes[1].routes) + 
    '</div>';
}
else if(route.changes.length == 2) {
    output = '<div class="col-xs-4">' + 
        renderRoute(route.from, route.changes[0], route.routes[0].distance, route.routes[0].routes) + 
    '</div><div class="col-xs-4">' +
        renderRoute(route.changes[0], route.changes[1], route.routes[1].distance, route.routes[1].routes) +
    '</div><div class="col-xs-4">' +
        renderRoute(route.changes[1], route.to, route.routes[2].distance, route.routes[2].routes) + 
    '</div>';
}

if(index == 0) {
    output = '<div class="panel panel-warning"><div class="panel-heading"><h3 class="panel-title">' + 
    '<span class="glyphicon glyphicon-star"></span> Recommended Route</h3></div><div class="panel-body row">' + 
    output;
}
else {
    output = '<div class="panel panel-default"><div class="panel-body row">' + output;
}
```

Okay, I'm a hypocrite. I only had 24 hours to write this and I 
cut some corners. REACT TAKES LIKE **6 HOURS** TO SET UP, OKAY? 

I'm sorry. :C

(It took a couple of days of hard toil to finally convert the UI 
code to React. I would never have made my self-imposed 24 hour 
deadline had I gone with React the first time.)

Why's half of router.js stolen code?
------------------------------------

Let's face it, we all do this. Copy stuff *gedi pitin* from 
StackOverflow. I just linked back to the sources, legal 
ramifications be damned.

Is this bus thing the only good thing you've written? Are you flogging a dead horse?
------------------------------------------------------------------------------------

I wouldn't call it good, but yes.

What now?
---------

I've barely tested it, so I'll probably make some tweaks here 
and there. The code, as usual, is on [Github and MIT licensed][6].

TL;DR
-----

[Go to this page, and it'll throw you not great bus route suggestions][5]

[1]: https://janithl.blogspot.com/2011/07/bus-route-finder.html
[2]: https://github.com/janithl/Bus-Route-Finder
[3]: http://chavs.000a.biz
[4]: https://github.com/janithl/BusRouteJS/commit/eac72894410693c47426720e240a8d5719316b1b
[5]: https://janithl.github.io/BusRouteJS/
[6]: https://github.com/janithl/BusRouteJS