---
layout: post
title:      "The First Project:  Unexpected Struggles "
date:       2020-06-19 19:13:03 +0000
permalink:  the_first_project_unexpected_struggles
---

The CLI Gem Project finally done, I've been reflecting on what I learned, and how it differed from the Labs that make up the bulk of learning at Flatiron.    The CLI project was one of the longer more difficult things I've undertaken, and yet strangely I didn't want to stop.  I wanted to keep working.  It didn't matter whether its the next project, or to add a new feature.  The fact that I have the power to create something using text, an editor and the command line is intoxicating.   Oddly enough, the implimentation of the app was fairly easy.
### Planning
One thing I found difficult was the transition from planning to implementation of the code.  My first idea involved printing lists of appropriate ski resorts based on skier difficulty using a ```scraper```.  I had found my website, but put less effort into determining whether I could effectively scrape the site before fully implimenting my classes.  When it came time to build the ```scraper``` I realized that the site was no good for the purpose I had in mind. This resulted in significant lost time and effort, but was an excellent learning experience.  

After the initial failure, I decided that I would look for an ```API``` that was open, didn't require an account, and had good documentation.  After a fairly exhaustive search I found the [Open Trivia Database](http://https://opentdb.com/).  It was exactly what I was looking for - the DB is open, and has extensive documentation and provides an HTML interface to play with the API and see what you are having returned. 

At this point planning was easy:  I knew the data I was using, and was able to quickly build my ```Category``` and ```Question`` classes.  I knew that ```Category``` had many ```Questions``` and ```Questions``` belonged to a ```Category```.  From there on I needed an ```ApiManager``` to deal with communicating with the ```API`` and a ```CLI``` class to control the UI/UX.  A little bit of legwork was all I needed to effectively and quickly turn a concept into a fully implemented ruby app. 
### Filtering out UNICODE
My second major challenge involved dealing with ```UNICODE``` characters.  Since the Trivia Database would only return encoded ```UTF-8``` strings, I struggled to find ```gems``` that could effectively do it.  In the end, I had to build my own ```Filter module``` and pass all strings through it.  

The one downside (or upside if you really like trivia) is that I have had to run through the app hundreds of times in order to find special characters and build my filter.   As each one comes up in the text, I add it to the filter.  I have managed to catch most of them now, however every now and again I see a new one.  The good news is I actually understand how ```UNICODE``` is represented now:  always starts with ```&``` and ends with ```;```, the text in between represents the modified letter and how its modified...  for example ```&ouml;``` means ```UNICODE``` the letter "o", and "uml" for umlaut (a way of expressing a vowel in German or Hungarian).    My ```Filter``` takes characters that can't be displayed and replaces them with the closest ASCII (console/terminal readable) character.  In the case of ```&ouml```, I replace it with an o.  

```Filter``` module below.  Its not pretty, but it works well. 

```
module CliTrivia::Filter

  # A method available to all classes that passes in a string and replaces unreadable characters with escaped
  # punctuation.  Used by question text and answers.
  def format_string(fsg)
    fsg = fsg.gsub(/&quot;/, "'")
    fsg = fsg.gsub(/&amp;/, '&')
    fsg = fsg.gsub(/&ograve;/, 'o')
    fsg = fsg.gsub(/&ouml;/, 'o')
    fsg = fsg.gsub(/&oacute;/, 'o')
    fsg = fsg.gsub(/&atilde;/, 'a')
    fsg = fsg.gsub(/&uuml;/, 'u')
    fsg = fsg.gsub(/&Ouml;/, 'O')
    fsg = fsg.gsub(/&prime;/, "'")
    fsg = fsg.gsub(/&Prime;/, '"')
    fsg = fsg.gsub(/&iacute;/, 'i')
    fsg = fsg.gsub(/&aacute;/, 'a')
    fsg = fsg.gsub(/&eacute;/, 'e')
    fsg = fsg.gsub(/&#039;/, "'")
    fsg = fsg.gsub(/&ldquo;/, '"')
    fsg = fsg.gsub(/&rdquo;/, '"')
    fsg = fsg.gsub(/&rsquo;/, "'")
    fsg = fsg.gsub(/&lsquo;/, "'")
    fsg = fsg.gsub(/&ntilde;/, 'n')
    fsg = fsg.gsub(/&lrm;/, '')
    fsg
  end
end
```

## Conclusion

All in all, I thougth it was a fun project, and a very worthwhile learning experience.  Not only did I have the opportunity to build a ruby gem from scratch, but I learned a few lessons along the way on how to be more effective and more efficient.  Now that this is done, I am excited to get started on the next project!!  Until next time.. 

