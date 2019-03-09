Title: The Lastfm Dataset
Date: 2016-07-20 09:09
Category: General
Tags: data, music

![Lastfm Reminder]({filename}/images/todoist-lastfm.png)

*Todoist reminding me that my Last.fm analysis is overdue*

I downloaded my [Last.fm scrobble data](http://www.last.fm/user/JanithL) a week
or so back using [this excellent online tool](https://benjaminbenben.com/lastfm-to-csv/). 
It contains almost every song I listened to on my PC (and some from my phone 
and iPod) between March 2011 and November 2014, 12784 scrobbles in total.

I will do a proper analysis *soon* (sorry, Todoist), but here are some 
descriptive stats that [Pandas](http://pandas.pydata.org/pandas-docs/stable/) 
throws out:

```
             Artist         Album         Title          Timestamp
count         12784         12593         12784              12784
unique          354           752          2048              12709
top     The Beatles  Past Masters  Sleeping Sun  09 Feb 2013 13:24
freq           1904           285            39                  8
```

I want to do an analysis of how I discovered and fell in love with new bands 
over the course of these three years. I don't listen to music as much these 
days, but this is a good dataset and I promise not to let it go to waste.

**Update:** Added the frequencies and histograms for artists and song titles.

Artists
-------

```
>>> df.Artist.value_counts()
The Beatles                        1904
Coldplay                            842
John Mayer                          604
Oasis                               499
Arctic Monkeys                      447
The Who                             345
The Rolling Stones                  318
Snow Patrol                         315
The Velvet Underground              297
Bob Marley & The Wailers            287
Noah and the Whale                  280
The Kooks                           246
Norah Jones                         211
The Kinks                           201
Badfinger                           189
Paul Simon                          179
The Jimi Hendrix Experience         160
Pink Floyd                          159
John Lennon                         146
Queen                               141
The Wailers                         140
Radiohead                           127
U2                                  121
Cream                               114
George Harrison                     111
Lorde                               100
Bee Gees                             97
Simon & Garfunkel                    92
Roy Orbison                          92
Billy Joel                           92
                                   ... 
```

[![Artist Histogram]({filename}/images/artist-histogram.png)](https://janithl.github.io/images/artist-histogram.png)

Song Titles
-----------

```
>>> df.Title.value_counts()
Sleeping Sun                         39
Could You Be Loved                   38
Parachutes                           35
Stuck on the Puzzle                  34
You've Got to Hide Your Love Away    34
Word                                 34
Brothers & Sisters                   34
My Girl                              32
One Day                              32
Wild Thing                           32
Bigger Than My Body                  32
Junk of the Heart (Happy)            31
Stir It Up                           31
Blue Skies                           31
Day Tripper                          31
Don't Look Back in Anger             30
No Woman No Cry                      30
For You (Shiver single Version)      30
All Around the World                 29
Strawberry Swing                     29
Lifeboats                            28
Let Me Go (acoustic)                 28
Ruby                                 28
Baby You're a Rich Man               28
Bitter Sweet Symphony                28
In Repair                            27
Getting Better                       27
Rainy Day                            27
Love Is All Around                   27
Here Comes the Sun                   27
                                     ..
```

[![Song Title Histogram]({filename}/images/song-title-histogram.png)](https://janithl.github.io/images/song-title-histogram.png)