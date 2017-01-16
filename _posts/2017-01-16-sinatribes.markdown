---
layout: post
title:  "Lemme tell you 'bout SinaTribes..."
date:   2017-01-16 17:41:35 -0500
---


## SinaTribes is a tribe-building simulation game!

Have you ever wanted to create (and grow) a tribe of "human beings"?

Have you ever wanted to crudely manage the collective lives of a small group of "arguably real" "people" with "state of the art" tables, buttons, and input fields?

Have you ever wanted to attack, talk to, and trade with other tribes, managed by people you don't know, over a basic and uninspired (yet web-*TASTIC*) user interface?

Well, **NOW YOU CAN**!

Visit SinaTribes (currently hosted [here](https://enigmatic-plateau-45553.herokuapp.com/)) to follow along. Or, click [here](#installation) to try to host it yourself. For a little more info on the guts of the application, click [here](#structure). The code for SinaTribes can be found on GitHub, [here](https://github.com/kjleitz/sinatribes).

## Playing the game


### Getting started

When you first navigate to the website, you are given two options: sign up, or log in. Sign up if you don't have an account, or log in if you already do (don't worry, passwords are hashed!). You don't have to give it your real email address, if you aren't comfortable with that. Just go ahead and make a dummy one and _no one will ever know_.

The assumption here, given that you're reading this README, is that you've never played the game before. So, in that case, you will be presented with your home screen—this is where you can manage all the tribes you have created. Currently, you have none. So, click the "New tribe" button to get started (alternatively, click on "World" in the top right to view the other tribes active in the world of SinaTribes, then click "Create a tribe" right next to that link to continue here).

Now, you're presented with a tribe creation page. You can choose a name for your tribe (woefully uncensored) and a religion (learn how to make suggestions for new features like "I want Wicca in the game. _WHY ISN'T WICCA IN THE GAME?_" by clicking [here](https://github.com/kjleitz/sinatribes#contributing)). Then, press "Create tribe" to found your new community.

If you have made your tribe's name too long, you will see that I... poorly designed the CSS and damn it I should fix that overlap now. My suggestion: Make your tribe's name shorter! At least until the dumb maintainer _(curse you, maintainer!)_ fixes the issue. If you don't see the issue, then I lied and there are no bugs in this game at all. _Ahem._

After creating your tribe, you are brought to the Tribe Management page. Before we explore this, go back to your user home page (click the big "Sinatribes" home link/logo in the top left). Create a new tribe so I can show you about "active tribes". Go ahead, I'll wait.

Done yet? Great! You're so good at this. Now, go back to your user home page again, and see that there's a button on your old tribe that says "Make active tribe". You can only have one active tribe at a time, but you can switch them easily (and as often as you'd like) with this button. Try it now!

#### Active tribes

Your "active tribe" is the one you will send messengers from (if you would like to interact with other tribes) or attack from (if you would like to make other tribes angry at you). Switch them around from the user home page (the big "SinaTribes" link up in the top bar). It also governs which tribe has a quick link to the tribe management page in the top right navigation menu, and which tribe's messenger activity the "Messengers" link (in the same nav) brings you to.

### Tribe management

You can get back to your tribe management page from a few places, which are self-explanatory once you see them. The easiest way to do so, however, is to click your tribe's name in the top right navigation menu. This brings you to your active tribe's management page.

Right now, you'll see a few different tables. Depending on the size of the screen you're using, they may be arranged a few different ways. I'll assume you're on a pretty sizable screen since that's the norm these days. If you're on mobile, it shouldn't be too hard to pick up on what I'm referring to.

#### General info

At the top left, we have the General Information table. This shows... general... information... about your tribe. You can buy land here. You'll want land because 1) you have a chance of randomly discovering resources as your expand, and 2) keeping your population density under 50 people per square mile keeps them happy.

Your technology score currently doesn't do anything. I kept it there as a reminder that all you suckers are still _tribes_, so don't start getting cocky once you have a spread of land and buildings rivaling that of NYC.

#### Census

Below the general info table is your Census info. Here, beyond the helpful data provided to you, you can enlist warriors, invite farmers, and ordain priests. Right now, you'll only see the option to invite farmers. You can have up to ten farmers per hut you build.

You get the options to enlist warriors and ordain priests once you have built barracks and a temple. We'll get into building buildings in a bit.

##### Farmers

Farmers, beyond padding your population, give you increased output from farms, yielding more food per farm when harvesting if you have excess farmers per farm. I'm leaving it up to you to figure out exactly how much more. Also, again, you can only have up to ten farmers per hut so they don't get all claustrophobic and mad at you. They're a little prissy.

##### Warriors

Warriors can only be enlisted if you have built at least one barracks. They add to your offensive and defensive strength scores, which add considerable weight to the random outcomes of raids. We'll get more into those later. They also make your tribe feel more protected, which adds to your population's happiness. Each costs $50 to enlist.

##### Priests

Priests can only be ordained if you have built at least one temple. They add to your tribe's happiness. They also contribute _significantly_ to your defensive score if you have a _heckuva_ lot of them, but you didn't hear that from me. If you have, again, a _heckuva_ lot of them (metric units), you get a little defensive help from _THE GODS&trade;_. Each costs one cloth to ordain.

#### Finances

Over to the right we have three more tables. One is finances. Shows your GDP and your collectible taxes. You can collect more taxes the more farmers you have, the happier your people are, and how many of certain buildings you own. I'll let you figure that out. You can collect taxes from your population once every five minutes.

#### Resources

Below that table, we have two more. These tables will grow and shrink as you play. The one on the left is your resources. It displays how many of each resource type you currently have. It doesn't display resources you do not _yet_ have.

You get resources from buying up land (you have a chance to discover certain types of resources), using buildings (see the next section), from gifts brought by messengers (we'll get to that later), and by winning raids (offensively or defensively).

#### Buildings

To the right, there is an infrastructure table. This shows the buildings you own. You can build buildings with the drop-down menu at the bottom of the table. Buildings cost a monetary amount and a resource amount. Go ahead and buy a few. Most have behind-the-scenes uses (e.g. walls and hospitals increase your defense, barracks increase strength and allow you to enlist warriors, etc.) but some have interactive uses. For example, mines will allow you to collect "mine-able" resources such as stone, iron, and coal, whereas farms will give you food, and factories will give you cloth. Experiment and see where this takes you.

#### Military

Smack dab in the middle is a table for your military information. This table displays your offensive score (this is matched up to another tribe's defensive score if you raid them) and your defensive score (do I have to say this again?). These scores do not deterministically decide the outcomes of your battles (as in, it's not purely checking your attack score against their defense score), but they heavily weigh them one way or the other. We'll get more into that when we talk about raids.

The "War messages" area displays the outcomes of recent battles you may have waged or been subject to. Check here for changes after you've raided a tribe, or periodically to see if you have _been_ raided.

### Messengers

You can view your messenger activity (the messengers you've sent or received) if you click the link in the middle of the tribe management page. Alternatively, click the "Messengers" link at the top right to go to your active tribe's messenger activity.

Messengers can be sent from tribe to tribe to relay messages or send gifts. You can send one from the World page, a user's page, or a tribe's public page (which can be accessed through the World page, most simply).

#### Gifts

You can send a message with your messenger, and you can also attach a gift to the little guy. Your gift can be comprised of money, warriors, and/or one resource. You can't send anything you don't have, so DON'T BOTHER.

#### Messenger activity

Once you've sent a gift, you can see the status of your recently sent messenger through the messenger activity page. This page lists your sent messengers and your received ones.

Here, you can view messages and gifts from other tribes, accept gifts from received messengers, reject messengers to be passive aggressive to their home tribe, reclaim gifts from messengers of yours which have been rejected by their destination, and see when someone has _rudely_ taken your gift yet rejected your messenger.

Hope that last one doesn't start a war!

### Raids

Speaking of war, let's talk about raids.

You can attempt a raid on another tribe (with your active tribe) by going to that tribe's page and clicking "Attempt to raid tribe". Careful! This can be dangerous. Try to estimate their strength. If you think you can handle it, go for it.

The chances of beating another tribe are random. However, those chances are weighted proportionally toward the attacker if their offensive score is greater than the defender's defensive score, and vice versa. Your offensive score is determined by a bunch of different factors, including number of warriors, happiness (for morale), and having certain types of buildings (like barracks). Your defensive score is the same way, but determined by different types of buildings (walls, for example) and there's a special case if you have a buttload of priests. But that's hard to do (and sustain).

If you win a raid, you receive 25% of their resources, randomly selected, as well as 50% of their money. On the other hand, if you lose a raid, you lose 90% of your warriors, and 90% of your iron, stone, and wood, and the defender picks it up from the battlefield. So, be careful about who you attack. There's some real risk there.

You can see the results of your raids (and raids you have defended against) in the "War messages" part of your military table, on your tribe's management page. You can clear those messages, too, if you _just want to forget_.

### Public tribe pages

You can see how other users see your tribe by going to your tribe's public-facing page. Click the name of the tribe on your management page to get there.

You can see other tribes by clicking their name wherever there is a link on it (the World page, their user page, your messenger activity page, etc.).

<a name="installation"></a>

## Installation

If you want to install the game and try to host it on your own, clone this repository:

```
git clone https://github.com/kjleitz/sinatribes
```

You're going to need to install and set up postgres if you haven't already:

[Install PostgreSQL](http://lmgtfy.com/?q=how+to+install+postgres)

Alternatively, to use sqlite3, put this in `config/environment.rb`:

```ruby
ActiveRecord::Base.establish_connection(
  :adapter => "sqlite3",
  :database => "db/#{ENV['SINATRA_ENV']}.sqlite"
)
```

right below the line that says:

```ruby
Bundler.require(:default, ENV['SINATRA_ENV'])`
```

Then, delete `config/database.yml` and `config/puma.rb`, and you should be able to run it locally with `rackup`.

Either method you choose (postgres or sqlite3), you'll need to `rvm install 2.2.5`, `rvm use 2.2.5`, then run `bundle install`. You can create and seed the database with `rake db:create`, `rake db:migrate`, and then `rake db:seed`. Then, finally, serve the site locally with `rackup`.

If you care about session security (like if you're _not_ running it locally), you should set an environment variable for the session secret (e.g. `export SECRET="some secret string"`) before you serve the site.

<a name="structure"></a>

## Application Structure

### Models

The foundation of SinaTribes is the various models for the elements of the game. These are classes inheriting from `ActiveRecord::Base`. They model each of the basic structured "things" in the game: user, tribe, population, religion, type of building, a tribe's ownership of a building, resource, messenger, a messenger's gift... These are comprised of the basic logic needed to create, associate, edit, read, and destroy objects of these classes.

Encapsulating logic into these classes allows the rest of the app to ignore low-level manipulation of the interacting objects. Instead, these classes expose a small surface area to the rest of the program, with an API that allows other pieces of the app to run general operations on the objects. This makes it easy to change the _way_ an object gets manipulated, all in one place, while elsewhere in the program it would seem that nothing has changed (because access remains the same).

### Controllers

The controllers manage routes and requests, and are separated into specific domains (user actions, tribe actions, and messenger actions) to simplify things. They all inherit from a main controller which itself inherits from `Sinatra::Base`.

The main application controller sets some configuration settings common to all the controllers, as well as some conditions which help reduce complexity in the other controllers. For example, `logged_in: true` passed to a routing method will ensure that it only occurs if the current user is logged in. `logged_in: false` does the reverse. The condition `current_user_tribe` allows a route method to be executed or not based on whether the URL tribe "slug" is owned by the current user. It also sets the `@tribe` instance method in the process so that you don't have to find the tribe a second time within the route's block. Super useful!

### Views

The views are templates specific to the different pages that need to be displayed on the website. They have minimal logic (minimal is a strong word), and they only access data from instance variables passed into them (only is also a strong word).

Each erb template inherits from a default `layout` in the root of the `views` directory. This layout, `layout.erb`, is the only view which accesses data beyond what is given to it in instance variables. It accesses the `flash` and `session` objects, as well as the `current_user` helper method, all directly. I made this choice because this layout is used _regardless_ of what route you're rendering it from, so it doesn't always know what it's getting. Ensuring data is passed to it from an instance variable each time is a lot of overhead and isn't very DRY.

### Structural changes

I'm going to have to redesign a bit of the database, unfortunately. I did two things that did _not_ keep scalability in mind. I made resources into individual objects/records, and I made building ownerships individual records as well.

Why is that bad? Well, first, for my pride's sake, let's go through why those two choices might be _good_.

#### The Good

This allows resources to be transferred like commodities. That's awesome! Not only are we modeling the resource objects on the real world, like good object-oriented programmers, we also save a bit of work in transferring resources between tribes. Currently, a resource has a name, an (optional) owner, and an (optional) gift it's attached to. This means that when you want to put a resource on a gift, you just change the `gift_id`. Easy peasy. If you want to transfer the resource to another tribe, just change the `tribe_id`. Again, easy. Create them as you need them, destroy them as you use them, all of the common actions take very little code.

If you _didn't_ do it that way, you can imagine storing resource information in, say, an inventory-style hash on a tribe (or gift). That means (probably) storing the data as JSON in an extra column, with resource names as keys, and amounts as values. That's all well and good, but say you need to add new resources? You'll have to access the hash, change the resource value, save the hash. That's not bad. What about if you need to transfer resources? You need to access the hash of the source tribe, verify there are enough resources to transfer, reduce the value, access the other tribe's hash, increase the corresponding value, validate that both operations worked fine, and reset if not. At least, that's my thinking. That goes for transferring from tribe to tribe, or tribe to gift to tribe, etc. Anything that needs to use resources will be using this logic.

Less important is the choice to have building ownership represented by individual database records. This choice was made as opposed to storing individual buildings as their own records, with ownership, and it was chosen instead of an "inventory hash" for mostly the same reasons as with resources. It's easy to create a "tribe building" and then just assign your tribe's id to it. 

To be fair, I'm just complaining for the sake of complaining. All this logic can be added to the models pretty simply, I think, and it probably won't change the API for the controllers to use.

#### The Bad

And it _will_ need to be changed. I've had three users (one brother, one friend, and one friend-of-a-friend) get... um, a little _too_ good at the game. I didn't put as much effort into _balancing_ the game as I did into _building_ the game, so once they started getting mega-rich, they started churning out resources and buildings like nobody's business. It wasn't until then that I realized that having resources and building ownership set up like this was a bad and _SUPREMELY UNSCALABLE_ idea. I've had to declare them "winners" and simultaneously nuke all their resources and buildings to make sure Heroku wouldn't shut off access to my database for going over the row limit for hobby projects.

#### The Ugly

I don't like declaring anyone "winner" except _me_, so this has to change.

I implemented a few changes that should stymie the issue, such as having limits on how many resources you can own, and having cooldown timers on using buildings to generate resources. But having inventory-style hashes stored on the tribes are probably a better idea in the long run.


