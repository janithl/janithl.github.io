Title: Remove shadows and uneven lighting from photographs of writing on paper
Date: 2021-12-09 19:15
Category: General
Tags: design
Slug: remove-shadows-and-uneven-lighting

This is mostly a note to self. You know how you often have photographs
of notes or forms that you need to print out, and there's a shadow or
uneven lighting across the image which makes the print look bad?

![Initial image]({filename}/images/shadow-removal/photo-1.jpg)

These are the steps I take to make something like this friendlier for a
black-and-white printer. I am using the amazing online editor
[Photopea][1], but most image editors can handle this.

### Initial image adjustments

First, desaturate the image. Since we're going to print it out in b&w anyway,
it doesn't matter. Bump up the contrast and brightness a bit too.

![Desaturated image]({filename}/images/shadow-removal/photo-2.jpg)

If the editor has a way to warp transformation or something similar, you can
use it to straighten out the image a little bit.

![Warped image]({filename}/images/shadow-removal/photo-3.jpg)

### Duplicating the layer

Now, duplicate the image layer. Invert the colours and apply a Gaussian
blur (I used about 7 pixels as the blur value)

![Blurred image]({filename}/images/shadow-removal/photo-4.jpg)

We can then change the layer mode from "normal" to "colour dodge"

![Layer mode screen shot]({filename}/images/shadow-removal/screenshot-1.png)

![Colour Dodge applied]({filename}/images/shadow-removal/photo-5.jpg)

### Final adjustments

Then with some level adjustment, we can get the final output to look evenly
lit and appropriate for printing.

![Level adjustment screen shot]({filename}/images/shadow-removal/screenshot-2.png)

![Level adjusted image]({filename}/images/shadow-removal/photo-6.jpg)

---

This is simply what worked for me, but there must be tons of other, _better_ ways
of doing this. Play around with the level adjustment, drop the bumping of
brightness and contrast at the start, and you might get something that works
best for the photographs of notes that you have.

[1]: https://www.photopea.com/
