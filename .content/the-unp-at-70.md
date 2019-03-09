Title: The UNP at 70
Date: 2016-09-11 09:05
Category: General
Tags: data, politics

![The Elephant]({filename}/images/unp-elephant.png)

The United National Party turned 70 this week. I thought I'd take a look at their electoral 
record, for funsies.

The data for this (short) analysis was sourced from Wikipedia. That data was in turn sourced 
from Department of Elections PDF files. I didn't cross-check the numbers because this is a 
blog and there is no accountability. `¯\_(ツ)_/¯`

I'll only be looking at General Election data because that's the only election that matters. :P

Election|Leader*|Valid Votes|Votes Won|% Votes|Total Seats|Seats Won|% Seats|W/L
-------:|:------|----------:|--------:|------:|----------:|--------:|------:|:-----:
1947|D. S. Senanayake|1,887,364|751,432|39.81|95|42|44.21|W
1952|Dudley Senanayake|2,327,626|1,026,005|44.08|95|54|56.84|W
1956|John Kotelawala|2,647,247|738,810|27.91|95|8|8.42|L
March 1960|Dudley Senanayake|3,041,420|909,043|29.89|151|50|33.11|W
July 1960|Dudley Senanayake|3,076,869|1,144,166|37.19|151|30|19.87|L
1965|Dudley Senanayake|4,046,720|1,590,929|39.31|151|66|43.71|W
1970|Dudley Senanayake|4,991,798|1,892,525|37.91|151|17|11.26|L
1977|J. R. Jayewardene|6,243,573|3,179,221|50.92|168|140|83.33|W
1989|R. Premadasa|5,596,468|2,838,005|50.71|225|125|55.56|W
1994|D. B. Wijetunga|7,943,706|3,498,370|44.04|225|94|41.78|L
2000|Ranil Wickremesinghe|8,647,668|3,477,770|40.22|225|89|39.56|L
2001|Ranil Wickremesinghe|8,955,869|4,086,026|45.62|225|109|48.44|W
2004|Ranil Wickremesinghe|9,262,732|3,504,200|37.83|225|82|36.44|L
2010|Ranil Wickremesinghe|8,033,717|2,357,057|29.34|225|60|26.67|L
2015|Ranil Wickremesinghe|11,166,975|5,098,916|45.66|225|106|47.11|W

A *win* is when the UNP went on to form a government. This was sometimes done by forming 
coalitions (e.g. in 1965).

Some Descriptive Statistics
---------------------------

```
>>> df['% Votes'].describe()
count    15.000000
mean     40.029333
std       7.121773
min      27.910000
25%      37.510000
50%      39.810000
75%      44.850000
max      50.920000
```

On average the UNP won 40% of the vote, with a fairly low deviation from that 
norm. The percentage of seats it has won has varied wildly from 8.4% to 83.3% 
(in the infamous 1977 election), mostly thanks to the winner-takes-all craziness 
of the *First Past The Post* electoral system.

```
>>> df['% Seats'].describe()
count    15.000000
mean     39.754000
std      18.945885
min       8.420000
25%      29.890000
50%      41.780000
75%      47.775000
max      83.330000
```

Some Interesting Notes
----------------------

* Sri Lanka, at least electorally, is not a [two-party system][0]. The UNP only won 
the majority of the popular vote on two occasions (1977 and 1989), and both under 
extraordinary circumstances. In 1977, the country was emerging from an unpopular 
experiment with a strictly-controlled, statist economy. The 1989 election was held 
during an extremely violent period of the country's history (more on that below).

![UNP Percentage of Valid Votes]({filename}/images/percentage-valid-votes.png)

* The percentage of the popular vote mattered little in the [First Past The Post][1]
system. The election was essentially a series of isolated local contests to win a 
particular electorate. It is even more surprising, then, to see that the UNP has only 
managed to win absolute majorities in only 3 of the 15 elections we looked at, and 
only twice under the FPTP system. 

![UNP Percentage of Seats]({filename}/images/percentage-seats.png)

* In the [1947 election][4], 29.11% of the popular vote and 21 (of 95) seats were won 
by independent candidates. One wonders how Sri Lankan electoral history would've evolved 
if [Proportional Representation][2] was introduced during this time.

* 1977 remains the UNP's biggest electoral victory. The UNP won 50.92% of the 
popular vote and a 5/6th majority in parliament. The biggest win ever recorded (in terms 
of the popular vote) by any party though was [6 years ago, by the UPFA led by Mahinda Rajapaksa][3], 
which managed to win 60.33% of the popular vote.

* Two of the UNP's most celebrated leaders, J. R. Jayewardene and D. S. Senanayake, 
have both only led a single election each, winning comfortably. J. R. avoided having the election 
due for 1983 by sneakily [holding a referendum to extend the term of the 1977 parliament][9]. 
D. S. fell off a horse.

* The term *leader* becomes a bit muddled (like everything else) after the Executive
Presidency is created. In 1989, R. Premadasa was the leader of the UNP but wasn't running 
for the post of Prime Minister, and after the 1994 election Gamini Dissanayake went on 
to become the Leader of the Opposition (over Ranil Wickremesinghe, the previous UNP 
Prime Minister).

* Ranil Wickremesinghe has led the UNP at 5 General Elections, winning twice. If he leads 
the UNP at the next General Election, he'll surpass Dudley Senanayake (5 elections, 3 wins) 
as the UNP leader who's led at the most number of General Elections.

* In the First Past The Post era, the UNP frequently won the *plurality* of the 
total vote, but lost the election thanks to the way electorates and the system was 
structured. Note the discrepancies between percentage votes and percentage seats, and 
the drastic reduction after Proportional Representation was introduced in the 80s:

**Before PR:**

Election|% Votes|% Seats|% Diff
-------:|------:|------:|------:
1947|39.81|44.21|4.40
1952|44.08|56.84|12.76
1956|27.91|8.42|19.49
March 1960|29.89|33.11|3.22
July 1960|37.19|19.87|17.32
1965|39.31|43.71|4.39
1970|37.91|11.26|26.65
1977|50.92|83.33|32.41

**After PR:**

Election|% Votes|% Seats|% Diff
-------:|------:|------:|------:
1989|50.71|55.56|4.84
1994|44.04|41.78|2.26
2000|40.22|39.56|0.66
2001|45.62|48.44|2.82
2004|37.83|36.44|1.39
2010|29.34|26.67|2.67
2015|45.66|47.11|1.45

![Vote/Seat Diff]({filename}/images/vote-seat-diff.png)

![Vote Percentage vs Seat Percentage under different systems]({filename}/images/votes-vs-seats-vs-system.png)

* The number of valid votes increased from just under 2 million in 1947 to 11 million in 2015. 
The troughs of 1989 and 2010 are also interesting, because these elections took place under
extraordinary circumstances. In 1989, there was a [full-blown insurgency ravaging the south][5],
and 2010 was the year after the [Sri Lankan Civil War][6] was finally concluded. 

![Valid Vote Growth]({filename}/images/valid-votes.png)

Swings
------

Election|Vote Swing|Seat Swing
-------:|---------:|----------:
1952|4.27|12.63
1956|-16.17|-48.42
March 1960|1.98|24.69
July 1960|7.30|-13.24
1965|2.12|23.84
1970|-1.40|-32.45
1977|13.01|72.07
1989|-0.21|-27.77
1994|-6.67|-13.78
2000|-3.82|-2.22
2001|5.40|8.88
2004|-7.79|-12.00
2010|-8.49|-9.77
2015|16.32|20.44

* In terms of vote swing (the different in percentage votes between the current and last election), 
the *'revolution'* of 1956 was the UNP's biggest defeat, losing 16.17% of its previous vote share.

* After the poor showing of 2010, 2015 was (surprisingly) the UNP's biggest gain yet, with a 16.32% 
increase. It edged out the 13.01% increase of 1977.

![Vote Swing]({filename}/images/vote-swing.png)

* In terms of seat swing (the different in percentage seats won between the current and last election), 
1956 was again the biggest loss (-48.42%). The UNP went from the 54 seats won in 1952 to a mere 8.

* 1977 was the biggest gain at 72.07%. The UNP went from having won 17 (of 151) seats in 1970, to 140 
(of 168) seats - J. R.'s infamous 5/6th majority.

![Seat Swing]({filename}/images/seat-swing.png)

Data Viz
--------

Making these graphs in [Seaborn][7] took a helluva long time, mostly because I am incompetant. 
See, I even managed to misspell *incompetent*.

Here's the code for the vote/seat difference graph:

```python
import matplotlib as mpl
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd

df = pd.read_csv('unp.csv')
sns.set(style="whitegrid", font="Georgia")

plot = sns.barplot(x="Election", y="Diff", data=df, color="forestgreen")
for i in plot.get_xticklabels():
        i.set_rotation(90)
sns.plt.show()
```

And for the Vote Percentage graph:

```python
import matplotlib as mpl
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd

df = pd.read_csv('unp.csv')

df['50 Percent'] = df['Valid Votes'] / df['Valid Votes'] * 50;
df['100 Percent'] = df['Valid Votes'] / df['Valid Votes'] * 100;

sns.set(style="whitegrid", font="Georgia")

# Initialize the matplotlib figure
f, ax = plt.subplots()

sns.barplot(x="100 Percent", y="Election", data=df, label="Valid Votes", color="grey")
sns.barplot(x="50 Percent", y="Election", data=df, label="50% of Valid Votes", color="white")
sns.barplot(x="% Votes", y="Election", data=df, label="Percetage of Votes Won", color="forestgreen")

# Add a legend and informative axis label
ax.legend(ncol=1, loc="upper right", frameon=True)
ax.set(ylabel="Election", xlabel="UNP Share of Votes")
sns.despine(left=True, bottom=True)

plt.show()
```

And the vote and seat swing graphs:

```python
import matplotlib as mpl
import matplotlib.pyplot as plt
import seaborn as sns
import pandas as pd

df = pd.read_csv('unp.csv')
sns.set(style="whitegrid", font="Georgia")

df["swingVotes"] = df["% Votes"].diff(1)
df["swingSeats"] = df["% Seats"].diff(1)

# replace swingSeats with swingVotes for vote swing graph
ax = sns.barplot(y="Election", x="swingSeats", data=df, color="forestgreen") 
sns.plt.show()
```

The data I used is in [a publicly shared csv file][8]. Consider everything MIT Licensed.

<script>
window.onload = function() {
   $('table').addClass('table table-bordered table-condensed'); 
}
</script>

[0]: https://en.wikipedia.org/wiki/Two-party_system
[1]: https://en.wikipedia.org/wiki/First-past-the-post_voting
[2]: https://en.wikipedia.org/wiki/Proportional_representation
[3]: https://en.wikipedia.org/wiki/Sri_Lankan_parliamentary_election,_2010
[4]: https://en.wikipedia.org/wiki/Ceylonese_parliamentary_election,_1947
[5]: https://en.wikipedia.org/wiki/1987%E2%80%9389_JVP_insurrection
[6]: https://en.wikipedia.org/wiki/Eelam_War_IV
[7]: https://stanford.edu/~mwaskom/software/seaborn/
[8]: https://gist.github.com/janithl/ea79a2bd330e71f7a6ce6644927e152f
[9]: https://en.wikipedia.org/wiki/Sri_Lankan_national_referendum,_1982
