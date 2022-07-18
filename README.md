# [Congress first said (in development)](https://twitter.com/congress1stsaid)

#### [derived from](https://maxbittker.github.io/nyt-first-said/)

The bot tracks when the Congressional record first publishes a word in history.

This code is still in development, so bugs beware.

The code takes steps to throw away un-interesting words like proper nouns and urls, but picks up a lot of typos and nonsense. Sanitization is an ongoing process.

This fork is inspired by Allison Parrish's @everyword bot, the [NewsDiffs](http://newsdiffs.org/about/) editorial change archiving software, the [NYT first aid bot](https://maxbittker.github.io/nyt-first-said/)

## Basic architecture

congress-first-said is essentially a single script. It's intended to be run at regular intervals (may require a cloud service.)

`parsers/congress.py` is a beautifulsoup parser adapted from the [newsdiffs sourcecode](https://github.com/ecprice/newsdiffs). 

## Future pieces (in dev)
`scrape.py` will check for new record urls, retrieving the article text using `congress.py`, splits them into words, and then determines whether each word is fit to tweet using (in this order) and some heuristics to discard unwanted types of words. Since there's no Congressional record API (is there?) this checking process requires further optimization. If all of these checks pass, it will ultimately tweet the word and any links.

`api_check.py` uses the [NYT article_search API](https://developer.nytimes.com/) to check through all digitized NYT history to be confident this is really the first occurrence of a word. It returns weird 500s for some words. If you know why let me know. For our case it may not be needed (or useful). Time will tell.

## Again - this is a work in progress.

## dev notes

`environment.yml` holds the libraries installed in a python environment (you'll need conda+pip due to some packages being not on `conda-forge`).