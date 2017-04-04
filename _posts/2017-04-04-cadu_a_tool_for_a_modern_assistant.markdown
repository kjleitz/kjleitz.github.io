---
layout: post
title:  "Cadu, a tool for a modern assistant"
date:   2017-04-04 07:11:11 -0500
---


## Whaddaya mean, "modern assistant"?

Sometimes there's not enough time in the day to finish all the mundane things on your to-do list. Sometimes it's just been a rough day. You'd rather not have to research and buy the cheapest tickets and hotel rooms for that trip you have coming up. You don't have time to be on hold for an hour just to get that little piece of information from your ISP. You have too many things going on to remember your daily schedule, and setting reminders yourself has proved inconsistent.

Don't you wish you had a personal assistant? They could get all those little things done for you. But _man,_ that would be expensive. You don't need a personal assistant, you just need a couple things done a day, just to make your life a little easier.

So, how do you make a personal assistant affordable? Maybe one assistant can assist more than one person. With few enough tasks, maybe one assistant can help _ten_ people. Maybe _fifteen!_ At a tenth the cost, an assistant might be affordable to a large population.

So, how can a personal assistant help that many people? If they only accepted tasks that could be done remotely, which is nearly everything these days, they'd be able to stay in roughly one spot all day and hammer out tasks like nobody's business.

But hey, looks like it's somebody's business, now!

[Cadu](https://github.com/kjleitz/cadu#cadu) is the interface between a new type of personal assistant and that assistant's clientele. Using Cadu, an entrepreneurial person who is _good_ at getting things done can become a personal assistant to a bunch of people who are _bad_ at getting things done, but who cannot quite afford an actual assistant.

In the past, such an assistant would have had to build their own website from scratch, or rely on unwieldy methods of communication with their clients, like a mix of email and electronic calendars. But now, all you have to do is set up Cadu, and bam! You're in business.

## Cool! ...so how does it work?

Cadu sorta acts like an interactive to-do list. If you're a client, you list out all your tasks for the day (or week, month, etc.). You set due dates, categorize them with labels (e.g., "telephone call", "typing", "purchase", etc.), and add details. As you go about your business, you mark the individual tasks complete as you finish them. For some tasks, you might want some assistance. You can press a button labeled "Request Assistance", and Cadu will alert your assistant to the request. After that, you'll get color-coded notifications when the status of the task changed (i.e., yellow for "accepted", blue for "in progress" and green for "complete"), and they drop to the bottom of the list and turn gray when you click them. You can also get a measure of the progress of a task by similarly-colored circles on the task itself.

There are also some purposeful avenues of communication between a client and an assistant, which focus/organize correspondence to specific subjects and areas. You can get reminders from your assistant for things you need to get done, and you can dismiss them once they've been read. You can also add information about tasks in comment sections attached to the task card, and your assistant will be able to read and respond to those comments in a thread with a dedicated subject (that is, the task), as long as you've requested assistance with that task.

There's a good measure of privacy between users, too. An assistant can only see the tasks which you request of them. Clients cannot view the profiles, tasks, or comments of other clients, and an assistant can only view those who are their clients.

On the assistant's side of things, the interface is very similar. The tasks that are shown to you (as an assistant) are your clients'. You don't create tasks yourself, but you are sent ones that your clients have requested of you. You have the ability to accept the task, mark it as "in progress", and mark it complete. Automatic notifications are sent to the party who the notification concerns (for example, an assistance request notification would be sent to you, the assistant, but when you accept a task, a notification saying as much will be sent to the client it concerns). You have the ability to send reminders to a client, too, which you can associate with a task for easy linking (those are color-coded as well, just like the notifications). If you need more information about a requested task, you can ask in the comment section for that task, and you can have a discussion there until the task has been completed. The other party will always be notified when one comments, so no comment will go unnoticed. You can view all of your tasks at once (sorted by next due), you can view your tasks by client, or you can view them organized by label (maybe you want to get all "telephone call" tasks finished in one batch).

## Should _I_ use Cadu?

Cadu was built for a specific purpose. It enables someone (or a group of similarly-minded people) who wants to start a personal assistance business to instantly get off the ground. By setting up Cadu and directing clients to the site, they can quickly create a sustainable and growable business with a tool that facilitates a focused and organized approach to task management. Without Cadu, it would be exceedingly difficult to keep track of so many clients, all their tasks, all their varied communication platforms, and the frequently insufficient, tangential, or opaque messaging that wastes time and creates confusion. With Cadu, everything is in one place: detailed instructions, focused discussion, bi-directional progress tracking, automated notifications, and manual reminders. If that sounds like what you need, then yes, you should try Cadu!

## How do I get this thing up and running?

You can see instructions for installing and trying out Cadu [here](https://github.com/kjleitz/cadu#cadu)! If you're comfortable with using the command line, you shouldn't have much trouble.

## ...will you own part of my business?

Nope! Cadu is free and open source. If you can make use of it, I'm happy to have helped. If you do use it, be sure to let me know! I'd love to hear how it works out for you.

## What a great idea! How can I help?

See [here](https://github.com/kjleitz/cadu#contributing) for details on contributing. This project is open source (under the MIT license) and [hosted on GitHub](https://github.com/kjleitz/cadu), so pull requests, bug reports, and suggestions are welcome!
