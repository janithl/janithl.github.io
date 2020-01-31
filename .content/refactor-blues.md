Title: My 2020 guide to rewriting a piece-of-shit codebase
Date: 2020-01-31 15:32
Category: General
Tags: code, work
Slug: refactor-blues
Subtitle: I failed hard so you don't have to

![Soptair Enjiniya]({filename}/images/engineering-meme.jpg)

<p class="text-center">Meme by
<a href="https://www.facebook.com/JusticeForTharindu/photos/a.594439464358595/806533719815834/?type=3&theater">Justice For Tharindu</a>
</p>

**First, you need to make up your mind.** If you take this project on you _must_
proactively try to make things better. How to do this will depend on a number of
factors and the support of the stakeholders, but you must _actively try_ to make
the codebase a _better place_, or you'd come to the end of your 2 or whatever
years looking after this garbage dump and not have anything good to show for it.

**Understand the system.** Learning the codebase might take time, but try to
figure out what the overarching concepts, the business logic, and how users
actually want to achieve. What users want to do with the system and what the
system currently does might be misaligned, so porting the thing with warts and
all into a shiny new shell might not make sense.

**Try to get the stakeholders onboard.** Try to make a point about how the
shittiness of the current system is costing them customers and money. Businesses
usually care about reputation and the bottom line, so you have to make your case
in lingo they understand. Show them the numbers, show them how it could all be
better.

**Break down the system into parts.** Moving everything wholesale into the new
system is not going to be practical in most cases. See where you can start
porting right now, and get to work. Things that could be services on their own,
like reporting, exports, and external integrations, are good places to start.

**Write tests.** If I could go back in time and teach my older self anything,
it's the value of writing tests first before getting down to implementations.
This one thing will make your code more reliable and add value. In the case of
a rewrite, this is even more straightforward: the user journeys are already
concrete and you can easily write test cases for them to guide the new
implementation.

**Get your team excited.** This has gone on long enough and I know you guys are
fatigued, but we can work together and make life less shit for ourselves and
our users. Try to understand their concerns and misgivings, but also don't
compromise in your quest to _make the world a better place_. They'll thank you
later.

<p class="text-center text-muted">* * *</p>

I always learn these lessons too late, when the chance for me to act on them
has passed. But hey, maybe it'll come in handy someday.
