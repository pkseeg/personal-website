---
title: I made twitter write some poetry
subtitle: And it wasn't really that difficult

# Summary for listings and search engines
summary: I trained a character-sequence RNN deep learning model to write poetry based on famous English poets. I then used the twitter API to build a feedback loop between my poetry model and twitter, so essentially twitter (geolocated in the USA) was writing poetry.

# Link this post with a project
projects: [twitter-poetry]

# Date published
date: "2021-05-19T00:00:00Z"

# Date updated
lastmod: "2021-05-19T00:00:00Z"

# Is this an unpublished draft?
draft: true

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**Craft Your Content**](https://www.craftyourcontent.com/writing-with-robots/)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags:
- Deep Learning
- Natural Language Processing
- Natural Language Generation
- Twitter
- Poetry

categories:
- Deep Creativity

# [LINK](https://pkseeg.com/)
# {{< youtube HluANRwPyNo >}}
# **bold**
# _italics_
# {{< figure src="image.png" title=IMAGE" >}}
---

## Background ##
This week I completed a pet project that I've been thinking about for some time. I'm fascinated by the intersection of AI and creativity. AI is already on its way to doing many tasks at a superhuman level, and superhuman creativity is likely the final frontier. I've seen some pretty cool projects like [1 The Road](https://en.wikipedia.org/wiki/1_the_Road#Reviews) and [Deep Art](https://deepart.io/) (neural style transfer), and I've always wanted to try my hand at something like that. I've been particularly interested in poetry for awhile - I've taken some creative writing courses and I was the poetry editor of my high school's literary magazine.

This project is nowhere near the same quality as 1 The Road or Deep Art, but I do think it has conceptual value. The idea was to connect twitter to a poetry-writing deep learning model, looping between the two and gathering the poetry output.

## Process ##
Essentially, this is what I did.
1. Gathered poems from many famous English language poets ([from this corpus](https://github.com/sravanareddy/rhymedata))
  1. Cleaned the poems
2. Built a character-sequence RNN for next character prediction and trained it on the poems
3. Built a system to connect the twitter api search function to the RNN in a feedback loop

This system
* Searches and gathers the top tweets for a given keyword
  * this keyword begins as 'solstice'
* Chooses a tweet string to use as the input to the RNN
  * This choice is weighted by the total engagement of the tweets
* Gathers a random amount of model output
  * Frequently repeating model output strings
* Selects a new keyword from the model output
* Repeats for a random number of iterations

And, _voila_. Twitter writes poems.

## Examples ##
Here are a couple poems written by the system. I just chose lines from the poems for titles. Can you tell where the twitter strings are incorporated?

### That tower ###
```
And in a think own never give my love from a room.--That tower
And ends of link, I man, Finds, follow's, what only.
And how spring, and district thought not how genes,
To Feature, and thinks engine;
So the years and his betting hill
To be us thy which works and singer;
Where frames thing in the blood.
```
### Congratulations ###
```
An' his could printed that the thinks airs,
Had (the turn name low the from the Horns:
And the chow'd we main turned any.
A my cunporth her taught, and event,
Of a taste, for can not Congratulations to the team for winning the 2021 UEFA Women's Champions League Final! You've inspired unto him all News
His range, hollow other center with al, and fence,
The Flows their hired beauty it Men;
And Sin making can ray. And all Dead
This should apperious bank anthight the.
The Next, dead her mouthed the help contest her come and been wilt be,
And fire points his Ole of anchor its love,
And the round mars to Snake the world me many his are.
```

## Thoughts ##
The poems are not good, but I was pleasantly surprised at how many words came out in English given the obvious limitations of the simple RNN. Some of the lines _feel_ poetic, too, even if the 'thoughts' aren't fully formed - "Where frames thing in the blood."

I'd like to take this idea and keep moving forward with it - for starters, using a more modern LSTM and a more complex twitter scraping methodology. Maybe one day we'll have AIs that write our poetry for us. Maybe I'll write one of them.
