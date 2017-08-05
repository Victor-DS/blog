---
layout: post
title: "Soccer and Probabilities: Gathering the data"
date: 2017-08-05 12:00:00
categories: statistics
featured_image: /images/cover.jpg
---

A pre-requiste to build a predictive system is to have data to analyse. **Lots** of it, preferably. So, how do we get it?

Basically, we need to do three things: 
1. Find where the data is available.
2. Scrap that data.
3. Store it in a way we can use later.

## Find

That was trickier than what I assumed at first...

First thing I thought was: *Well, I could just find a public API and get it*.

No big deal, right? Well... Turns out there was no such thing. No, seriously. Brazil, the country of football, and you couldn't even find a decent, public API to query past results! And I'm not even talking about historical data at this moment. Not even 2 or 3 years past championships.

So, it wasn't going to be *that* easy. Plan B was to find a website, and scrap it manually.

Luckily, there was the **Futpedia** project (which apparently is not maintained anymore). A website by *Globo* (a media conglomerate in Brazil) who had historical data from soccer matches from the 1900s until 2016.

The website was going on and off and had a few problems, but the data was there... And only there.

So... Let's scrap it!


## Scrap

Now to the fun part: Build a web scrapper to get **all** the data available.

The site was a mess. They didn't use the same standard for different years in the same tournament, the site would go up and down, and there was some really hacky stuff going on on that HTML...

Some data they just left in a Javascript variable in the HTML (yeah, really). So I just used some regex to get it, and Gson to parse it into a POJO.

Some other years was somewhat well structured and I managed to build a nice little scrapper using **Jsoup**.

But, since the data wasn't standardized (different names, some years had more info than the others, different structure, etc), I had to build a single and simpler data model for this, and parse this data into a unified model.

In the end I left both options there, one to get the *pure* data, and another to the standard and simplified model.

(And since the simplified had all the necessary information I was gonna need, that is what I'm using in the next steps!)


## Store

Having done the above, all I needed was to store it.

Since I just needed something quick and dirty, I just serialized it in a JSON and saved on my PC. That would allow me to easily import later when I build my prediction software, and took me seconds to do it using the Gson library.

And that was it! Took me a couple of days, but I had in my PC **about 100 years** worth of Brazilian soccer data. I had all the major regional, national, and international championships that Brazilian teams disputed in over a 100 years.

[The entire code is Open Source and available on my GitHub](https://github.com/Victor-DS/Futpedia-Scrapper).

I also made a web scrapper to get data more recent data (2017 and onwards) since the Futpedia website was not updated anymore. It takes the data from [Globo Esporte and it's also Open Source](https://github.com/Victor-DS/GloboEsporte-Scrapper).
