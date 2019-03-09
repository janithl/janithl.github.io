Title: Links: Machine Learning
Date: 2016-08-25 21:13
Category: Links
Tags: code, data, machine learning

I'm changing the format of the links posts to topic-based posts which I will 
add to over time. Seems like a better way to organize than basing them on dates.

August 2016
-----------

[*An exclusive inside look at how artificial intelligence and machine learning 
work at Apple*][1]

A fascinating look at how ML work is being done at Apple, and how it meshes 
with privacy of user data and the "Apple way" of absolute secrecy.

> Apple’s penchant for secrecy puts it at a disadvantage against competitors 
who encourage their star computer scientists to widely share research with the 
world. “Our practices tend to reinforce a natural selection bias — those who are 
interested in working as a team to deliver a great product versus those whose 
primary motivation is publishing,” says Federighi. If while improving an Apple 
product scientists happen to make breakthroughs in the field, that’s great. “But 
we are driven by a vision of the end result,” says Cue.

---

[*The 9 Deep Learning Papers You Need To Know About*][2]

A great overview of some recent breakthrough research in CNNs.

> [...] a lot of the new and important developments in the field of computer 
vision and convolutional neural networks. [...] The first half of the list 
(AlexNet to ResNet) deals with advancements in general network architecture, 
while the second half is just a collection of interesting papers in other 
subareas. 

---

[*Language Translation with Deep Learning and the Magic of Sequences*][3]

The magic of sequence-to-sequence learning, taking a crack at the 'holy grail'
of Computational Lingustics: Machine Translation

> What if we took two RNNs and hooked them up end-to-end? The first RNN could 
generate the encoding that represents a sentence. Then the second RNN could take 
that encoding and just do the same logic in reverse to decode the original 
sentence again [...] what if (and here’s the big idea!) we could train the 
second RNN to decode the sentence into Spanish instead of English?

With promising results:

> Machine learning researchers only invented this two years ago, but it’s 
already performing as well as statistical machine translation systems that took 
20 years to develop.

And wider applications:

> About a year ago, researchers at Google showed that you can use 
sequence-to-sequence models to build AI bots.

And: 

> [...] by replacing the first RNN with a Convolutional Neural Network [...] we 
can turn pictures into words (as long as we have lots and lots of training 
data)! 

> Andrej Karpathy expanded on these ideas to build a system capable of 
describing images in great detail by processing multiple regions of an image 
separately.

---

[*Text summarization with TensorFlow*][4]

I wish Google will stop stealing all our research topics. :P

> We’ve observed that due to the nature of news headlines, the model can 
generate good headlines from reading just a few sentences from the beginning of 
the article. Although this task serves as a nice proof-of-concept, we started 
looking at more difficult datasets where reading the entire document is 
necessary to produce good summaries. In those tasks training from scratch with 
this model architecture does not do as well as some other techniques we’re 
researching, but it serves as a baseline.

It feels like TensorFlow (and SyntaxNet) is really taking the NLP world by 
storm, especially looking at [Google's offerings at ACL 2016][5].

---

[*Segmenting and refining images with SharpMask*][6]

Not wanting to be left out, Facebook has also released some incredible research
in the past few weeks, earlier with [fastText][7] and now extending to DeepMask 
and SharpMask:

> DeepMask employs a fairly traditional feedforward deep network design. In such 
networks, with progressively deeper network stages information is more abstract 
and semantically meaningful. For example, early layers in a deep net might 
capture edges and blobs, while upper layers tend to capture more semantic 
concepts such as the presence of an animal's face or limbs. By design, these 
upper-layer features are computed at a fairly low spatial resolution (for both 
computational reasons and in order to be invariant to small shifts in pixel 
locations). This presents a problem for mask prediction: The upper layer 
features can be used to predict masks that capture the general shape on an 
object but fail to precisely capture object boundaries.

> Which brings us to SharpMask. SharpMask refines the output of DeepMask, 
generating higher-fidelity masks that more accurately delineate object 
boundaries. While DeepMask predicts coarse masks in a feedforward pass through 
the network, SharpMask reverses the flow of information in a deep network and 
refines the predictions made by DeepMask by using features from progressively 
earlier layers in the network. Think of it this way: To capture general object 
shape, you have to have a high-level understanding of what you are looking at 
(DeepMask), but to accurately place the boundaries you need to look back at 
lower-level features all the way down to the pixels (SharpMask). In essence, we 
aim to make use of information from all layers of a network, with minimal 
additional overhead.

They've also done some work on real time (video) classification:

> In addition, our next challenge will be to apply these techniques to video, 
where objects are moving, interacting, and changing over time. We've already 
made some progress with computer vision techniques to watch videos and 
understand and classify what's in them in real time.

[1]: https://backchannel.com/an-exclusive-look-at-how-ai-and-machine-learning-work-at-apple-8dbfb131932b
[2]: https://adeshpande3.github.io/adeshpande3.github.io/The-9-Deep-Learning-Papers-You-Need-To-Know-About.html
[3]: https://medium.com/@ageitgey/machine-learning-is-fun-part-5-language-translation-with-deep-learning-and-the-magic-of-sequences-2ace0acca0aa
[4]: https://research.googleblog.com/2016/08/text-summarization-with-tensorflow.html
[5]: https://research.googleblog.com/2016/08/acl-2016-research-at-google.html
[6]: https://code.facebook.com/posts/561187904071636/segmenting-and-refining-images-with-sharpmask/
[7]: https://research.facebook.com/blog/fasttext/