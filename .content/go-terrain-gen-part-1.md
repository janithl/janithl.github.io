Title: A basic terrain generator in Go (Part 1)
Date: 2019-09-17 21:12
Category: General
Tags: code, golang
Slug: go-terrain-gen-part-1
Subtitle: Ain't no mountain high enough

I haven't gushed about Go much on this blog[^1], but I thought of writing a
small series of posts on a little piece of code I cooked up while I was
supposed to be doing other, more important things[^2].

### Concept

So I was sitting there, zoning out and browsing [one of my favourite subreddits][1],
when I thought about how terrain can be generated. And I thought if we were to
take a flat plane that sliced through the mountains at progressively decreasing
heights, you'd first get a few isolated spots (the peaks of the mountains), and on
the next iteration you'd always have the areas adjacent to these peaks showing up
(because mountain tops don't float in thin air).

Computationally, if the map was a 2D array, we could randomly set a few elements
as peaks, and then generate the rest of the mountain around those "peak" elements.
Of course, with each iteration you would also have the possibility of running into
peaks that weren't high enough to be captured at the earlier iteration, so we
should keep randomly sprinkling peaks among the (not already assigned) elements
in the map.

### Pseudocode

The pseudocode for the most basic version would look something like this:

```
# map initialised to 0s
map[height][width]

for elevation <- 5 to 0
	for h <- 0 to height
		for w <- 0 to width
			# if element is already assigned value, skip
			if map[h][w] > 0
				continue

			# if array element next to higher elevation
			# or picked as a peak randomly
			if map[h][w] next to elevation + 1 or random()
				map[h][w] <- elevation
```

Seems simple enough, right?

### Go Implementation

The initialisations, loops and randomly picking an element to be a peak (and
printing the result out) seem straightforward enough, so let's get those out
of the way first and create our `main.go` file:

```go
package main

import (
	"fmt"
	"math/rand"
	"time"
)

const width, height, elevation = 16, 16, 9

// we set the random chance of a peak occuring to 5%
const peakProbability = 5

var fullMap [height][width]int

func main() {
	// rand needs to be seeded, so we set the current
	// nanosecond timestamp as the seed
	rand.Seed(time.Now().UnixNano())

	// iterate down from max elevation, assigning vals
	for e := elevation; e > 0; e-- {
		for h := 0; h < height; h++ {
			for w := 0; w < width; w++ {
				// if the element has already been
				// assigned, skip it
				if fullMap[h][w] > 0 {
					continue
				}

				// if the random value meets our criteria,
				// it's a peak
				if rand.Intn(100) < peakProbability {
					fullMap[h][w] = e
				}
			}
		}
	}

	// print out map
	for h := 0; h < height; h++ {
		fmt.Println(fullMap[h])
	}
}
```

We run the code with `go run main.go`, and get the following output:

![First Iteration]({filename}/images/iteration-1.png)

To quote Chernobyl[^3], it's "Not great, not _terrible_".

---

[In the next part][2] we'll look at a quick and dirty way to implement a
way to look at elements adjacent to our current element (the part of our
pseudocode that we didn't implement), and assign values to it—and better
visualisation of the terrain map.

[**The full code for this part can be found on Github.**][3]

[^1]: Mostly because this blog has been _inactive_ for the last 2 years, but
    more on that in a later post.

[^2]: My biggest gripe about my otherwise perfect workplace is that I don't
    get to write Go for a living.

[^3]: Which I haven't watched yet! 🙈

[1]: https://www.reddit.com/r/CitiesSkylines/
[2]: {filename}/go-terrain-gen-part-2.md
[3]: https://github.com/janithl/go-terrain-gen/tree/master/part1
