---
layout: post
title:  "So you made a CLI data gem, eh?"
date:   2016-11-28 04:13:58 +0000
---


I've been doing Flatiron School's [Learn.co](https://learn.co) for... let's see, two months now? Well, my first really open-ended project was assigned recently, which was to make a CLI app to scrape data from a public website. The app was to be written in Ruby, employ good object-oriented design patterns, and provide a user access to data some levels deep in a website through a command-line interface.

## Enter Whatsa

I chose to create an application I call "Whatsa". Check it out [here](https://github.com/kjleitz/whatsa) on my GitHub page.

### What's a Whatsa?

Whatsa is a CLI app that allows you to search a word or phrase and receive a quick summary about that subject.

### How does it do that?

It searches your query on Wikipedia and finds the page you're most likely looking for. If you've been somewhat vague, or your search term could refer to multiple things, it will ask you to select from a disambiguation of topics. Usually, however, your term will go straight to an article. Whatsa then gives you the first paragraph of that article (usually a surprisingly decent summary).

If you're not super satisfied with that bit of information (and you need to know a little more) you can type `more` to get a better picture of that subject. If you're _still_ not satisfied, and you want to know something _specific_ about the thing you've searched, type `other`, and it will list the categories of information Wikipedia knows about the subject (its "History", "Early Life", "Uses", etc.). You can select one of those sections, if you'd like, and it will give you the first paragraph of that section, too (which you can extend similarly with another `more` command). You can make a new query with `new`, ask for help at any time with `help`, or exit the application with `exit`.

Simple?

Simple!

## I get how it works, but how does it _work?_

Under the hood, Whatsa is all Ruby. It uses open-uri to fetch some HTML pages, and the Nokogiri gem to parse it.

### I am a metaphorical rowdy teen with behavioral issues. Give me some structure!

Ah, okay. I'll highlight some of the key pieces.

#### `Whatsa::Scraper` (#1)

The `Scraper` class is where it all begins. When you submit a search, a `Scraper` object is initialized with that query:

```ruby
WIKISEARCH = 'https://en.wikipedia.org/w/index.php?search='

# ...

def initialize(term)
  # only keep word chars and parens, turn everything between each 'word'
  # to a single '+' and remove '+'s at the beginning and end if they're there
  @query = term.gsub(/[^A-z0-9\(\)]+/, '+').gsub(/(\A\+|\+\z)/, '')

  # store the page in an instance variable so we don't keep polling the site
  @page = Nokogiri::HTML(open(WIKISEARCH + self.query))
end
```

The scraper is going to use the phrase you entered to construct a URL, from which it will grab the HTML page for your result. The way _you_ wrote the search phrase might not be well-formatted for inserting right into a URL, so we're gonna replace whitespace with `+` signs, and get rid of special characters (except for parentheses, gotta love those parentheses).

The scraper checks whether there's anything there (did you just mash buttons on your keyboard? There's no such thing as an 'akejscfn', you little...). If something _is_ there, it checks whether it's a results page (learn to be a little more specific next time, dummy), a disambiguation page (not your fault, the human race is just bad at coming up with unique names for things), or an actual article (good job, _NERD_, you knew what you were looking for!), and decides how to present that to you, the user (rhymes with loser! Okay, I'll stop, don't be such a baby).

In the case of a disambiguation page, the scraper will create a `Disambig` object. We'll get to the other cases in a bit.

#### `Whatsa::Disambig`

A `Disambig` object is initialized with a Nokogiri document representing its page:

```ruby
def initialize(noko_doc)
  @title = noko_doc.css('h1').text
  @items = noko_doc.css('#mw-content-text li')
  @descriptions = make_descriptions
end
```

It populates a list of search match possibilities based on the unordered list items on the page, and makes a hash out of those items consisting of the potential article name lifted from the first link (as the key) and its description from the rest of the list item (as the value). Check it out:

```ruby
def make_descriptions
  self.items.inject({}) do |memo, item|
    unless item.css('a').empty?
      key = item.css('a').first.text
      toc_link = item["class"] && item["class"].match(/toc/)
      dmb_link = key.match("(disambiguation)")
      all_link = key.match("All pages with titles")
      unless toc_link || dmb_link || all_link
        desc = item.text.split("\n").first.strip
        memo[key] = desc.gsub(key, "").gsub(/\A[^\w"]/, "").strip
      end
    end
    memo
  end
end
```

This hash is composed for the next step (from where we left off in the last section), which is presenting it to the user and asking for a choice. When a choice is made, the `Disambig` object creates a new `Scraper` object with that key as the search term, and tries to make an article out of the result.

#### `Whatsa::Scraper` (#2)

"Why would you initialize a _whole new_ `Scraper` object to make an article out of? You literally have the link right there in front of you! Go scrape that directly!"
    - You right now

I _hear_ you whining, but I _refuse_ to listen.

I have a very specific vision of how articles should be created and handled. It's part of my commitment to good ("good" might be a strong word) object-oriented code.

Nobody should be going around willy-nilly creating `Article`s on their own, or grabbing pages left and right without permission. That is a job for _ONE MAN_ and _ONE MAN_ alone, the all-powerful `Scraper` dude. We start getting `Article` objects from `Disambig` objects, and everything starts falling apart. Some people start communicating one way, some people another way, and we ruin our precariously balanced middle-school-social-studies-textbook-pyramid-graphic. We know our place in this society, and that place is _subordinate_ to our `Scraper` king.

So, yes, maybe it makes more sense to get the link directly and make a page out of it, but it turns out that if you search the words in the key exactly, you get the right article every time. "Every time", of course, is my own experience, but it's pretty darn consistent.

"Okay, well why don't you just pull the suffix of the link it points to, you know, the part of the article URL where it's the literal term you'd want to use to get that (and only that) webpage, and use that to build the `Scraper` object, instead of the potentially ambiguous hash key string?"
    - You right now

I _hear_ you whi... oh.

_Ahem_. Actually, that's a good idea. I should have done that the first time around, but good ideas aren't always your first ideas. I might do that sometime soon, but no promises. Seems to work just fine right now, so it's low on the priority list.

Where were we?

Ah, right. So, it made a new `Scraper` object out of that choice. We're right back where we were at the end of the "**`Whatsa::Scraper` (#1)**" section. We have a `Scraper` object and we wanna make an article out of it.

If we get a "search results" page, we're just going to take the first hit, _à la_ Google's "I'm Feeling Lucky". If we got a disambiguation page, we've already gotten the choice, and we have an article page from that, too. If we got _another_ disambiguation page from that choice, we're not gonna bother asking again. Let's just take the first hit on that one, too. If we've gotten an actual article page, we're hitting the ground running.

So, how does the `Scraper` actually make the article? It does it like this:

```ruby
def make_article
  if article?
    Whatsa::Article.new(self.page)
  elsif results_page? && !not_found?
    first_title = self.page.css('.mw-search-results li a').first.text
    self.class.new(first_title).make_article
  elsif disambig?
    self.class.new(make_disambig.choices.first).make_article
  else
    nil
  end
end
```

Each of those little boolean helper functions are pretty simple, actually, but separating them out into their own methods really makes the code readable, don'tcha think? Here they are, in case you were wondering:

```ruby
def results_page?
  !self.page.css('.searchresults').empty?
end

def not_found?
  !self.page.css('.mw-search-nonefound').empty?
end

def article?
  !self.page.css('#ca-nstab-main').empty? && !disambig?
end

def disambig?
  !self.page.css('#disambigbox').empty?
end
```

Turns out there are some pretty simple and unique elements on each type of page. Almost _just_ by checking to see if they're there, you can tell what kind of page it is.

#### `Whatsa::Article`

So, now we've made an `Article` object. It's initialized with a Nokogiri document, as well, representing its page:

```ruby
def initialize(noko_doc)
  @title = noko_doc.css('h1').text
  @contents = noko_doc.css('#mw-content-text').children
  @sections = make_sections
end
```

It gets the full text as an array-like collection of nodes in the `<div>` that represents the meat of the article, and stores it in the `@contents` instance variable. That collection consists of, most importantly, all the paragraphs and all the section names those paragraphs fall under. Those things are all we really care about. Then, we make some `Section` objects out of those contents:

```ruby
def make_sections
  indices = section_indices
  indices << -1
  secs = [Whatsa::Section.new("#{self.title} - Introduction", intro_pars)]
  indices.each_cons(2) do |i, j|
    title = self.contents[i].text.gsub('[edit]', '').strip
    par_nodes = self.contents[i...j].select { |e| e.name == 'p' && e.text != "" }
    pars = par_nodes.map { |par| par.text }
    secs << Whatsa::Section.new(title, pars).tap { |s| s.article = self }
  end
  secs
end
```

This code is a little bit tough to read, but it's made easier by separating some of the logic out into a couple helper methods. Basically, we construct a list with the index (in `@contents`) of each section heading, and grab all the paragraphs between each section heading as the "text" of that section. We initialize a new `Section` object with the title and the text, and add it to our `Article`'s list of sections.

The `Section` object is pretty simple, so let's take a look.

#### `Whatsa::Section`

A `Section` is initialized with a title and its constituent paragraphs (unlike the other 'page'-like objects which are initialized with a Nokogiri document):

```ruby
def initialize(title, paragraphs)
  @title = title
  @paragraphs = paragraphs
  remove_citations
end
```

The `Section` object is only ever used within an `Article`, which is why it's structured a little differently. A `Section` doesn't _have_ its own page. It's a part of its parent `Article` (which can be accessed by a `#article` getter/setter method). Its responsibilities are simply to yield a summary (its first paragraph) or the full text of the section (all of its paragraphs joined, separated by newlines).

It also removes citation marks when it can (you know, when there's a little superscripted link like this<sup>[[3]]()</sup> in a Wikipedia article, directing you to a citation footnote). You can't follow those links in Whatsa, so they just end up looking like scattered garbage. We remove them like this:

```ruby
def remove_citations
  self.paragraphs.map! do |par|
    par.gsub(/\[\d+\]/, "")
  end
end
```

Just a quick little regex to get any numbers in brackets and replace them with nothing. ...**_ABSOLUTELY NOTHING_, muah ha ha ha**...

#### `Whatsa::CLI`

So, we're pretty much all done. At that point, we've made an `Article`, we display the summary to the user (or the full text if they want more), and let them choose which `Section` to get the summary/full text from (again, if they want). Those interactions with the user are mediated by an instance of the `CLI` class.

We encapsulate all that logic in one simple `#run` method that our `CLI` object will be able to execute:

```ruby
def run
  welcome
  instructions

  loop do
    # get a search term
    input = ask
    scraper = Whatsa::Scraper.new(input)

    # get an article from the search, or restart the loop if it can't be found
    if scraper.not_found?
      puts "Hmmm... I don't know what '#{input}' means! Try something else."
      next
    elsif scraper.disambig?
      article = get_dmb_choice(scraper.make_disambig)
    else
      article = scraper.make_article
    end

    # summarize that article
    input = summarize(article)

    # the only valid input here that would go uncaught is "other", so
    # keep asking until you get a caught input (logic determined by
    # #gets_command, e.g. "help", "exit", "new") or "other"
    loop { input = input.downcase == "other" ? categories(article) : gets_command }
  end
end
```

There are a bunch of user interface methods in `Whatsa::CLI`, some mainly decorative and some logical. I won't go over some (`#welcome`, for example, displays a welcome message; `#ask` just prefixes asking for your input with "What would you like to know about", etc.), but here are some more important methods:

```ruby
  def gets_command
    input = nil
    loop do
      print "> "
      input = gets.strip
      case input
      when ""
        puts "Please enter a valid input."
      when "exit"
        exit
      when "help"
        instructions
      when "new"
        run
      else
        break
      end
    end
    input
  end
```

This method, `#gets_command`, is essentially a wrapper for the builtin `#gets`. We use this wherever we might want user input so we can handle default commands right away, no matter where we are asking for input! If some input is captured by the method (and is not `exit` or `new`, which closes the program, or starts it over, respectively), it will handle it and then ask for input again, eventually returning any un-captured input to where it was originally called. That way, if a user wants the instructions again, they can do so without it interrupting/restarting the program. They can continue right where they left off.

There are two points in the app experience where the user can choose between a list of possibilities (the disambiguation page and the sections of an article):

```ruby
  def display_dmb(dmb)
    raise TypeError unless dmb.is_a?(Whatsa::Disambig)
    system("clear")
    stripped_title = dmb.title.gsub("(disambiguation)", "").strip
    puts "Hmmm... #{stripped_title} could mean a few different things:\n"
    dmb.descriptions.each_with_index do |kvp, i|
      puts "#{i + 1}. #{kvp[0].to_s} (#{kvp[1]})"
    end
    puts "\nPlease select a choice, either by name or number."
  end

  def display_sections(text)
    text = text.article if text.is_a?(Whatsa::Section)
    system("clear")
    puts "Here are some specific subjects about '#{text.title}':\n"
    text.section_titles.each_with_index {|title, i| puts "#{i + 1}. #{title}"}
    puts "\nPlease select a choice, either by name or number."
  end
  
  # ...
  
  def categories(article)
    display_sections(article)
    choice = gets_command
    section = article.choose_section(choice)
    summarize(section)
  end
```

We put these into their own methods so we don't polllute the `#run` method with logic that can be separated into their own abstract divisions of labor.

We also have some quick little methods for summarizing/full-texting a section of an article:

```ruby
  def summarize(text)
    system("clear")
    puts word_wrap(text.summary)
    summary_helpline
    input = gets_command
    input.downcase == "more" ? full(text) : input
  end

  def full(text)
    system("clear")
    puts word_wrap(text.full_text)
    full_text_helpline
    gets_command
  end
```

These are useful because they separate the `more` command logic into a strictly summary-only scenario, so that doesn't have to be handled anywhere else.

The last method I'll go over is a purely decorative one, but it was fun to write and simpler than I thought it would be:

```ruby
  def word_wrap(text)
    count = 0
    words = text.split(/ /)
    words.each_with_index do |word, index|
      count += word.length + 1
      if count > 80
        words.insert(index, "\n")
        count = 0
      elsif word.index("\n")
        count = word.length
      end
    end
    words.join(" ").gsub(/^ /, "")
  end
```

This method, `#word_wrap`, simply makes sure the displayed text word-wraps to the next line at 80 characters in the terminal (as opposed to getting cut off in the middle of the word when a long string wraps to a new line). I'm only using it in the `#summarize` and `#full` methods, because that's where it's most obvious, but I'll likely push it onto all the text-displaying bits once I vet it more thoroughly (it took a _suspiciously_ short time to write last night at 3am, which makes me wary of throwing it around just yet). I originally tried to do it with a regex, but I couldn't figure out how to get it to preserve original newlines, so I just pull the text apart, word by word, like an enthusiastic investigator in the _Spanish Inquisition_ (which nobody expected, of course).

## Can you please be more specific?

No. Shut up. Go away.

## Any last thoughts?

A few. At least, I hope they aren't my last.

I learned a lot from this project. But it wasn't the usual "Oh, huh, I didn't know I could do that!" and "So _that's_ how that's done!"

Nope, I learned how to _do_ a project. I've never _completed_ something like this before. This project taught me the merits of writing tests before your code. It taught me how to organize and divide labor between different classes and objects, and the importance of modularizing code to make it easier to understand, write, fix, and maintain in general. I learned how to _start_ a project, with an outline and a vision and a structure, from scratch. That's big. There's a comfort there, a comfort I didn't have before.

So, I guess what I'm saying is, I'm comfy. Feels good, man.

Hmm... `whatsa comfy`?
