---
layout: post
title: Are you wasting your coding chops? Walk more, type less and still do more during your work day!
type: post
published: true
comments: true
tags: [automate, grunt, developer, rockstar]
---

<figure>
	<img src="../images/bot-beer-pour.jpg">
</figure>

With more and more of technology helping us finding and remembering things it is becoming increasingly difficult to rely
on people to remember things to do. Not that we didn't have this problem before. We've defined various workflows, processes
and standards for doing things precisely so we don't have to re-discover a problem. But those have steps you need to remember again.

As a developer, I never want to spend time doing things that a script or a software can do for me. But if you suffer 
from RSI the motivation to do this can be far greater. For example, I use Dragon NaturallySpeaking http://bit.ly/1UKpWxO 
for most of my blogs, including this one.

## Things that are tedious:
### Long commands
These  can be replaced by aliases,  in your favourite shell.

### Repetitive set of commands
You could write a shell script or any other script for that matter,  using your favourite language. 

### Build and deployment
This isn't really optional and you really need to make this for most production environments that need deployment at 
scale. I wanted to reiterate this here because this has other implications. You reduce the chance of missing things 
that are critical for example taking a database backup or copying the backup of the app before deploying the new so 
that you can easily revert back. 

You have no shortage of tools that you could pick from depending on your budget: Jenkins, Codeship, Bamboo etc. You could also roll your own!

### Code Reviews and QA
There is a huge list of things that you need to do as a developer and development team for the court to be production quality.  Here is a peek into what typically need to look into:
- All test cases pass
- Feature has been tested  in Chrome, Firefox and Safari and screenshots of the test result are added
- Each code change was executed
- Test cases have been added and test edge conditions
- This code was self-reviewed once for DRYness & quality
- All code linter issues are fixed that get reported by tools like [JsHint](http://www.jshint.com/docs/) or 
[Codenarc](http://grails.org/plugin/codenarc)
- User facing texts are checked for typos & grammar mistakes
- There has been a UI/UX test and is approved
- This was tested locally on a server eg: Tomcat

We use Trello, BitBucket, GitHub and Slack primarily for dev communication.  Three of these have APIs exposed that can 
be exploited to create automated checks so that somebody doesn't have to manually remind people to  complete an item 
on the checklist.

[Chrome extension complaining about kanban](https://chrome.google.com/webstore/detail/kanban-wip-for-trello/oekefjibcnongmmmmkdiofgeppfkmdii) flow when we go over our "work in progress" limit, to a Trello/Git bot complaining with a comment if things are missing; make our lives much easier. 

For example, if any of us moves a card to "Done" with a Pull Request with not adequate amount of reviews our Bot would complain
	Need to be at least reviewed by 2 reviewers

### IDE exploits
You are not really using the IDE you're just using it as a autocomplete. Using snippets to reduce typing boilerplate 
is essential to focus on solving the problem. Most IDE's or editors support some form of it. More info on snippet 
management for popular ones like [IntelliJ](http://bit.ly/1SZ8Vwm), [Eclipse](http://bit.ly/1SZ9436), 
[TextMate](http://bit.ly/1SZ982E), [Vim](http://bit.ly/1SZ96I6)

### Automate without coding
There are some neat tools available connecting multiple apps together like [Zapier](https://zapier.com/) can do things like
- Save gmail attachments to Dropbox
- Share tweets from a list on Twitter to Slack and back

### TL;DR
Automate the grunt; because it would be better if you spend your time, solving real problems!

Would love to hear how you cut out the grunt.
