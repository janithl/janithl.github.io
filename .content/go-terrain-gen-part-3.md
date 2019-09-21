Title: A basic terrain generator in Go (Part 3)
Date: 2019-09-19 20:49
Category: General
Tags: code, golang
Slug: go-terrain-gen-part-3
Subtitle: Take a look at me now

[In the last part][1], we refactored the code and added CLI flags. The output
right now looks like this:

![Compile and Output After Flags]({filename}/images/go-terrain-gen/p2-output-3.png)

It doesn't really give us a sense of what the terrain looks like, though. Let's
change that.

### Unicode

Unicode has some [nice characters][2] that can help us here. The ones we're
going to use today are:

```
U+2591      ░       Light shade
U+2592      ▒       Medium shade
U+2593      ▓       Dark shade
U+2588      █       Full block
```

We can update the `Print()` function to use these new shade blocks. We've also
added a space to get the "no shade" effect.

```go
func (f *fullMap) Print() {
	mapShades := [5]string{" ", "░", "▒", "▓", "█"}

	// print out map
	for h := 0; h < f.height; h++ {
		for w := 0; w < f.width; w++ {
			// print a space (black) if elevation is zero
			if f.elements[h][w] == 0 {
				print(" ")
				continue
			}

			// get the approximate shade nearest to the elevation number
			elementShade := float64(f.elements[h][w]) / float64(f.elevation) * float64(len(mapShades)-1)

			// get its index
			shadeIndex := int(math.Round(elementShade))

			// print out the corresponding unicode char
			fmt.Print(mapShades[shadeIndex])
		}

		// print a newline
		fmt.Println()
	}
}
```

Go takes its types very seriously, so someone coming from a dynamically typed
language like PHP or Javascript might be a bit confused. But trust me, it is well
worth the trouble to specify all the type conversions manually, as the compiler
helps you find bugs with data types that would otherwise plague you at runtime.

Let's compile and run it!

![Output after shades]({filename}/images/go-terrain-gen/p3-output-shades.png)

Very cool. I think it gives a good idea of how bad the generation algorithm
currently looks. 😅

### Colour

[Terminals support colour][3], and all you got to do is send an ANSI escape
sequence[^1] with your output. The colours I want to use are blue and cyan
for the sea and shallows, and green and yellow for the fields and mountains.
We'll modify `Print()` to add these and output the codes:

```go
func (f *fullMap) Print() {
	mapColours := [4]int{36, 34, 32, 33} // blue, cyan, green, yellow
	mapShades := [4]string{"░", "▒", "▓", "█"}

	// print out map
	for h := 0; h < f.height; h++ {
		for w := 0; w < f.width; w++ {
			// print a space (black) if elevation is zero
			if f.elements[h][w] == 0 {
				print(" ")
				continue
			}

			// get the approximate colour nearest to the elevation number
			elementColour := float64(f.elements[h][w]) / float64(f.elevation) * float64(len(mapColours)-1)

			// get the colour index
			colourIndex := int(math.Round(elementColour))

			// get the approximate shade within that colour
			elementShade := (elementColour - math.Floor(elementColour)) * float64(len(mapShades)-1)

			// get its index
			shadeIndex := int(math.Round(elementShade))

			// print out the corresponding ANSI code and unicode char
			fmt.Printf("\033[%dm%s\033[0m", mapColours[colourIndex], mapShades[shadeIndex])
		}

		// print a newline
		fmt.Println()
	}
}
```

We first get the colour index, and then get the shade index within that
colour. Let's compile and run it with the same flags as before:

![Output after colours]({filename}/images/go-terrain-gen/p3-output-colours.png)

Fabulous! ❤️💚💙

---

Being able to visualise your output is an important part of building any
program (which is a reason wireframes exist, I guess). With the graphics sorted,
[our next improvements][4] to the system[^2] will be more apparent when we
implement them.

[**The full code for this part can be found on Github.**][5]

[^1]: I learned this only _yesterday_! [Rosetta Code][6] has code on how it's
    done in all the languages.

[^2]: I'm planning to cover assigning values to elements near the peaks, and
    how introducing a bit of randomness will help make things more realistic.

[1]: {filename}/go-terrain-gen-part-2.md
[2]: https://en.wikipedia.org/wiki/Block_Elements
[3]: https://en.wikipedia.org/wiki/ANSI_escape_code#Colors
[4]: {filename}/go-terrain-gen-part-4.md
[5]: https://github.com/janithl/go-terrain-gen/tree/master/part3
[6]: https://rosettacode.org/wiki/Terminal_control/Coloured_text#Go
