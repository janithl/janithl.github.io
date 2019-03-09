Title: The month of Augustus
Date: 2016-07-31 22:41
Category: Personal
Tags: code, uni

It begins tomorrow, and I'm really excited because I've been FUP'd by SLT for
the last few days. It's been painful going, as `vnstat` attests:

```
         day         rx      |     tx      |    total    |   avg. rate
     ------------------------+-------------+-------------+---------------
     07/22/2016   410.55 MiB |   54.48 MiB |  465.03 MiB |   44.09 kbit/s
     07/23/2016   231.05 MiB |   36.32 MiB |  267.37 MiB |   25.35 kbit/s
     07/24/2016   620.32 MiB |   84.95 MiB |  705.27 MiB |   66.87 kbit/s
     07/25/2016   413.00 MiB |   59.05 MiB |  472.05 MiB |   44.76 kbit/s
     07/26/2016   392.72 MiB |   60.14 MiB |  452.86 MiB |   42.94 kbit/s
     07/27/2016   401.44 MiB |   64.09 MiB |  465.52 MiB |   44.14 kbit/s
     07/28/2016   264.50 MiB |   25.76 MiB |  290.27 MiB |   27.52 kbit/s
     07/29/2016   312.83 MiB |   53.04 MiB |  365.88 MiB |   34.69 kbit/s
     07/30/2016   439.92 MiB |   45.89 MiB |  485.80 MiB |   46.06 kbit/s
     07/31/2016   134.91 MiB |   36.42 MiB |  171.32 MiB |   17.74 kbit/s
```

I've been painfully made aware of how heavy Facebook is, when even scrolling
down the timeline for a minute or two and replying to a few messages can cost a
couple dozen MBs. Makes me wonder how I survived on those 1 GB limited SLT
connections back in the day. But back in the day developers cared about  making
their pages light, unlike now. Sigh.

I've been making progress on my thesis (or its lit review, rather). About 3
more papers and I can forward it to my supervisor for a read-through, I feel.
Very much relieved that I've been able to get this far on things.

Took a break from studies today (it *IS* Sunday) to do some work on [ol' 
Kottu][1]. Things have been broken a bit since [Twitter, true to form, 
deprecated useful functionality][2]. So I got rid of the Twitter share counting,
recalibrated the popularity calculation, and - since I was in there already - 
moved the front-end to use Bootstrap. Because slapping Bootstrap on sites that
have worked perfectly without it is my thing. I'm hoping to deprecate the JQuery 
Mobile-based Kottu Mobile site in favour of the responsive Bootstrap main site 
in the near future, if there aren't any protests and self-immolations.

![Kottu Desktop]({filename}/images/kottu-bootstrap-desktop.png)

![Kottu Mobile]({filename}/images/kottu-bootstrap-mobile.png)

**Update:** `vnstat` output since Aug 1 (this is why I can't have nice things):

```
         day         rx      |     tx      |    total    |   avg. rate
     ------------------------+-------------+-------------+---------------
     08/01/2016     1.48 GiB |  133.97 MiB |    1.61 GiB |  156.10 kbit/s
     08/03/2016   305.62 MiB |   44.76 MiB |  350.39 MiB |   33.22 kbit/s
     08/04/2016     1.19 GiB |  115.37 MiB |    1.30 GiB |  126.38 kbit/s
     08/05/2016     1.71 GiB |  174.64 MiB |    1.88 GiB |  182.12 kbit/s
     08/06/2016   603.21 MiB |   53.36 MiB |  656.56 MiB |   62.51 kbit/s
```

[1]: https://github.com/janithl/Kottu2012
[2]: https://blog.twitter.com/2015/hard-decisions-for-a-sustainable-platform