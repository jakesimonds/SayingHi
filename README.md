# SayingHi

This is a Potemkin Village of a project, I am trying to write 'hi' in the green squares where it shows your github activity. 


# June 29th
I am updating this readme with the following support documentation: 

<img src="figs/calendar.png" width=550>

For the record, I had the idea for this project after I noticed the first column three squares already existed, so this is sort of Day 2 of, oh shit I gotta do a git push today. 

While I'm here, wanna treat this is a kind of time-capsule/public journal/recording the State-of-Things-Now making this dumb project. 

### How I Got into Tech

I encountered github for the first time around two years ago. Was 'self-studying' over the summer, which basically meant sifting through marketing materials for boot camps and cold calling random friends and acquaintences who I thought might be in somewhat technical fields. 

Discovered Github at some point, but it was a bit of a disappointment then. The readmes were all written with assumed knowledge I didn't have, if I did even try to pull or fork anything I didn't get any futher than that, and it was all just very...confusing(sometimes still is). 

So then I almost did a bootcamp. Almost did two, one that would have started in July 2021, and another that would have started in September. This being 2021 they are all remote, which was one big reason I didn't bite the bullet. I was living with my parents, and, for the July one, I sort of did the math and realized that come December I would be: 10K-ish poorer, turning 30, living with my parents(having done this bootcamp, allegedly six hours of instruction or whatever a day, online, in my parent's house), and desperately looking for that first job. No thank you. 

I also should mention at this point two years ago I had the most money I'd ever had. Coffers are full. Coffers are full because of the Golden Unemployment of Covid, followed by full time employment while living with my parents, so what I did next was I went to Oaxaca, Mexico. My second or third day there I finished my application to Northeastern, which was a little daunting, because I was applying to Computer School and the form had a place to put Computer Experience and...

<img src="figs/Computer_Experience_Jake_Simonds.png" width=550>

I mean, looking at it now I really should have lied. Or been more creative. Now after 18 months of grad school I see software through a wider lens and could brainstorm all kinds of things I did in the first 29 years of my life that would have been relevant on a form like this (using weird ticketing software for theatre festivals, making and updating a website, blogging intermitantly, etc (if you, reader, are thinking about getting into tech that might be an interesting place to start. Where is interfacing with sofware (or hardware) already a part of your life?). But they did let me in, and so I started school January 2022. 

Grad school has been an incredible priviledge in that it's been a time where I haven't had to worry about anything other than my own learning, and I've been able to dive head first into this world that has been eaten by software. More on all that tomorrow, Saturday, and then in two weeks. 


# June 30th

I really like this panda. 

<img src="figs/child_panda.png" width=550>


It was made with stable diffusion, but as the result of tensor operations in an attempt to make meaningful changes to an image by making changes in the latent space of the text tensor. 

First, I made a (1,77,768) shape text encoding (using CLIP or whatever) of (call it dummy3) "painting of a normal sized panda bear". 

Then, I made two more text encodings, one (dummy1) for "painting of a normal sized polar bear", and one (dummy2) for "painting of a child-sized polar bear". 

Then, I iterated through dummy1 & dummy2 (all textual embeddings being the same shape), and when the raw tensor value for dummy2 was above some raw threshold, as well as greater than the raw value in the same spot in dummy2, I grabbed that value and its index in a hash map. 

Then, I iterated through dummy3 (our panda bear), and I did a lot of feature engineering so I honestly don't remember exactly what I did for this specific image, but I either straight up replaced the values that existed in the hashmap (made by comparing dummy1 to dummy2) when I got to those indices in dummy3, or I applied some scalar multiplication. 

None of this really worked the way I wanted to, but it felt so tantalizingly close, is my excuse why I don't remember exactly what feature engineering I was up to. 

My idea was to pass some essence of a concept only present in dummy2 on to dummy3, which I then actually turned into an image, using just tensor operations. 

<img src="figs/microscopic.png" width=550>

**dummy1 = "painting of a normal sized polar bear"**

**dummy2 = "painting of a microscopic sized polar bear"**

**dummy3 = "painting of a normal sized panda bear"**

**What's displayed: dummy3 ~+ (dummy1 ~- dummy2)**


<img src="figs/pineapple.png" width=550>


**dummy1 = "still life of banana and pineapple"**

**dummy2 = "still life of a banana"**

**dummy3 = "still life of a coffee mug"**

**What's displayed: dummy3 ~+ (dummy1 ~- dummy2)**

<img src="figs/banana.png" width=550>

**dummy1 = "still life of pineapple and banana"**

**dummy2 = "still life of a pineapple"**

**dummy3 = "still life of a coffee mug"**

**What's displayed: dummy3 ~+ (dummy1 ~- dummy2)**

These were the successful images. There were probably 50+ unsuccessful images, which only made these limited successes more maddening. 

The more I read about just how stable diffusion works the more I think my naive ideas are just that. But it is interesting. And confusing. 

Like, for instance, here is a grid of the same textual embedding just scaled by a factor from 0.4 to 1.1. 

<img src="figs/astro_horse_scalar.png" width=550>

I mean, like, I multiplied the entire embedding by some arbitrary value. And we end up with this weird progression from almost sketch to more realistic. But no Guassian noise present in any of the images. And all of them relatively intelligible. So it's the in the relative values of the tensors that the information is encoded? 

I'm phrasing that as a question because if anyone reading this has a sense of what's going on I'd really love to know lol. 

