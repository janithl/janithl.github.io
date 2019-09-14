Title: Some things I wish I knew as a young startup dev
Date: 2018-06-08 19:17
Category: General
Tags: code, people, work

As some of you might know, I started my career as the first
developer at a startup, way back in 2012. It was a challenging
but rewarding experience, and I got to learn a lot and explore
the full breadth of the software stack. The following are some
learnings that I wish I could tell my younger self.

### Prototype like your life depends on it

> “I know you guys are restless to get started, but before you
> write a single line of code — Make a prototype and run it by your client”

I heard this line from one of the co-founders of a very successful
software services company. In a startup, the client might be your
founder who’s sitting in the desk in front of you, but code is costly
to work and rework. Always prototype, at least on paper. It’ll help
everyone visualise what they’re building, and see issues and limitations
before you even start on the implementation.

![Paper Prototype]({filename}/images/paper-prototype.jpg)

<p class="text-center">Image by <a href="https://www.flickr.com/photos/21218849@N03">Samuel Mann</a></p>

### Write a spec, and check it twice

Software is all about the spec. It defines the scope and the tests that
need to pass to mark the work as done. A spec might be as simple as a user
story followed by some acceptance criteria in the [Gherkin format][1], but it’s
very important for estimations, avoiding the dreaded scope creep, and writing
high quality code.

**A sample spec:**

> As a **logged in user**,

> I want to **access the Account page**,

> so that I can **see my Account Settings**

**Acceptance criteria:**

> **Given** I am logged in as janith@startup.lk,

> and I am in the home page

> **When** I click on “Account” on the top menu,

> **Then** I am navigated to the “Account” page,

> and I can see my Account Settings.

Remember, you will most probably be your own QA, so write a solid automated
test suite that covers these conditions.

### Timebox, timebox, timebox

You probably won’t have a Project Manager, nor will anyone really care about
Agile or sprints. The constant mantra will be _“just get it shipped”_. This is
damaging in two aspects: a team without a welldefined end goal and a timeframe
to achieve it in will drift and probably get demotivated, and you will not be
able to set up a good measure of how much work your team is able to tackle in a
given period of time--which will make it really difficult to draw up a project
timeline.

![Sprint Plan]({filename}/images/sprint-plan.jpg)

Avoid this trap. Set up 1 or 2 week sprints, take up only stories that the team is
confident they can achieve in that timebox, and [**have a retro** at the end of each sprint
to discuss what went well, what failed, and how the team can improve][2]. Try your best to
ship production code at the end of every sprint. It will give the team a sense of
achievement, and [that which is most valuable: customer feedback][3].

### Know when to use Frameworks and Libraries

- There are some terrible frameworks.

- Often, code you write from the ground-up for a specific purpose will be faster and more performant.

Both of the points above a valid, and I avoided using PHP and frontend Javascript
frameworks for the longest time. This cost us a lot in terms of delivery speed and
maintainability, and especially made onboarding new developers hell. I still wonder
how things would’ve turned out had I used — say, Laravel or Python with Flask, or
KnockoutJS from the earliest days. We probably would’ve shipped a lot more features,
and at much higher quality.

### Read up, seek support

Look, when it’s a tiny startup and it’s just two junior devs fighting fires every
day, you will miss out on a lot. You won’t have leads who will guide you on best
practices and design patterns, or architects who explain why TDD is awesome, and
why you should read [Clean Code by Robert C. Martin][4].

It will be up to you to reach out: follow your [favourite][5] [library][6] [authors][7] on Twitter,
subscribe to a few good tech blogs on Medium and turn on the “Daily Digest” email.
Participate in the community and tech meet ups, and try to reach out to batch mates
or seniors working in bigger companies for advice and tips. There are so many people
willing to help if only you’d ask.

![Workshop]({filename}/images/workshop.jpg)

---

So yeah. Those are a few things I learned the hard way, and I wouldn’t trade it for the world. I hope you find it useful.

[_Originally Posted on Medium_][8]

[1]: http://docs.behat.org/en/v2.5/guides/1.gherkin.html
[2]: https://medium.com/softwaredevtools/agile-retrospectives-why-your-team-should-be-having-them-even-if-youre-not-in-the-tech-industry-b98c3df6501d
[3]: https://ma.tt/2010/11/one-point-oh/
[4]: https://www.goodreads.com/book/show/3735293-clean-code
[5]: https://twitter.com/dan_abramov
[6]: https://twitter.com/dhh
[7]: https://twitter.com/John_Papa
[8]: https://medium.com/@janithl/some-things-i-wish-i-knew-as-a-young-startup-dev-d6475d3f8151
