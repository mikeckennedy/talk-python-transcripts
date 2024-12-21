00:00:00 If you maintain projects on places like GitHub, you know that having a classy readme is important

00:00:04 and that maintaining a changelog can be helpful for you and consumers of your project.

00:00:09 It can also be a pain. That's why I'm excited to welcome Ned Batchelder to the show.

00:00:15 He has a lot of tools to help here, as well as some opinions we're looking forward to hearing.

00:00:20 We cover his tools and a bunch of others he and I found along the way.

00:00:24 This is Talk Python to Me, episode 395, recorded Monday, December 5th, 2022.

00:00:30 Welcome to Talk Python to Me, a weekly podcast on Python.

00:00:46 This is your host, Michael Kennedy.

00:00:48 Follow me on Mastodon, where I'm @mkennedy and follow the podcast using @talkpython.

00:00:53 Both on fosstodon.org.

00:00:56 Be careful with impersonating accounts on other instances.

00:00:58 There are many.

00:00:59 Keep up with the show and listen to over seven years of past episodes at talkpython.fm.

00:01:04 We've started streaming most of our episodes live on YouTube.

00:01:08 Subscribe to our YouTube channel over at talkpython.fm/youtube to get notified about upcoming shows and be part of that episode.

00:01:16 This episode is brought to you by the Local Maximum Podcast over at LocalMaxRadio.com.

00:01:22 And it's brought to you by Sentry.

00:01:24 Don't let those errors go unnoticed.

00:01:26 Use Sentry.

00:01:27 Get started at talkpython.fm/sentry.

00:01:30 Transcripts for this episode are sponsored by Assembly AI, the API platform for state-of-the-art AI models

00:01:38 that automatically transcribe and understand audio data at a large scale.

00:01:43 To learn more, visit talkpython.fm/assemblyai.

00:01:47 Ned, welcome back to Talk Python to me.

00:01:49 Hey, thanks for having me.

00:01:51 This is always fun.

00:01:52 Yeah.

00:01:52 And it's always a good time to have you on the show.

00:01:54 Got such interesting things to talk about.

00:01:57 I think we've previously spoken about coverage.py, beginners and experts,

00:02:02 and several other things probably if I go back through the old search engine.

00:02:07 I've had many opinions about many things.

00:02:09 Perfect.

00:02:09 Well, we're looking forward to hearing your opinions on...

00:02:14 The title might suggest on the ReadMe, but I think maybe we've got to expand it to a couple other markdown files,

00:02:19 maybe on a project as well to get the holistic picture.

00:02:22 But basically, we're going to talk about tools and ideas and techniques for making your project more accessible,

00:02:30 feeling more polished and welcoming to people when they land on your project on GitHub or GitLab or wherever.

00:02:37 So that'll be fun.

00:02:39 Yeah.

00:02:39 It's an interesting topic too, because as a project maintainer, there's all this project level automation that goes on,

00:02:45 and there are all these fascinating tools to get parts of it done in different ways and competing philosophies.

00:02:50 Yeah, absolutely.

00:02:50 I know some of them because I fork different projects, and then I'll sync it or something,

00:02:56 and it'll say that my automation couldn't run.

00:02:58 I'm like, well, that wasn't my automation, but that's okay.

00:02:59 It's fine if it runs or it doesn't run.

00:03:02 I'm just here to follow.

00:03:03 But before we get into all that, maybe let's just do a quick recap for those of you,

00:03:08 those listeners out there who don't know you.

00:03:10 Maybe what's the elevator pitch, and what have you been up to the last six months or so?

00:03:13 So I've been working in the Python world for a very long time.

00:03:17 I don't know, 20 years now or something crazy like that.

00:03:20 But my day job is at edX, which is part of 2U now, an education tech company.

00:03:27 And I do open source logistics there.

00:03:30 edX.org runs an open source software that we've created called Open edX,

00:03:34 which also runs a couple of thousand other sites.

00:03:36 And my main day job is making sure that that collaboration continues well

00:03:42 between the people inside 2U and the people out in the community.

00:03:46 So it's an interesting dynamic of open source.

00:03:49 But on the side, I also maintain a number of projects, including coverage.py, which has been going for 18 years now

00:03:55 and is used by a lot of people.

00:03:57 So that's a whole other kind of open source that I do in the Python world.

00:04:01 Yeah.

00:04:02 That's a really rewarding job, right?

00:04:03 It's not optimizing ad clicks or other things like that, right?

00:04:07 It's helping people.

00:04:08 Right.

00:04:09 It's a noble goal.

00:04:10 We're educating the world and we're giving away software to help other people educate the world.

00:04:14 Yeah.

00:04:14 It's really good.

00:04:15 Yeah.

00:04:15 Fantastic.

00:04:16 And, you know, and speaking of open source projects, I think we might touch on a couple more of yours as we get going.

00:04:23 Yeah.

00:04:24 They tend to multiply somehow.

00:04:26 I haven't learned my lesson yet.

00:04:28 Yeah.

00:04:28 Just got these puppies running everywhere.

00:04:30 I don't know what's going on.

00:04:31 That's right.

00:04:31 Exactly.

00:04:31 They breed.

00:04:32 I don't know when it happens.

00:04:33 They breed.

00:04:33 Exactly.

00:04:34 All right.

00:04:35 Well, let's start off with one.

00:04:36 I don't know if you're familiar with this.

00:04:38 Readme.so.

00:04:40 I don't know what the SO stands for, but I think of this as readme as a service.

00:04:44 Interesting.

00:04:45 Yeah.

00:04:45 Or Stack Overflow.

00:04:46 No, .so isn't Stack Overflow.

00:04:48 I don't know.

00:04:49 I don't know why they chose .so.

00:04:50 I don't either.

00:04:51 The woman who maintains it works at GitHub.

00:04:53 I'm pretty sure.

00:04:53 We're going to find out when I get to the bottom.

00:04:55 But I don't think it has an association with Stack Overflow.

00:04:58 Right.

00:04:59 And usually two letters are country codes.

00:05:02 I don't know what SO stands for.

00:05:03 I don't either.

00:05:04 As a country.

00:05:04 Sorry, .so, folks.

00:05:06 But this place, readme.so, it says, this is the easiest way to create a readme.

00:05:12 Now, before we get into the details of this, maybe we should just talk about, you know,

00:05:16 let me pull up coverage.

00:05:17 Coverage.py on GitHub.

00:05:20 Not to put you on the spot or anything.

00:05:22 I don't mean to do that.

00:05:23 But let's just talk about what kind of stuff should you put on your project.

00:05:26 And like I said, we're going to have to expand a little bit.

00:05:29 Like, for example, there's tags and there's a link and there's should you have releases

00:05:34 shown and other stuff that you might kind of think of what you get when you land on a project.

00:05:39 So maybe start there with kind of how you think about what should be here.

00:05:43 Then we'll talk about some of the tools.

00:05:45 The first thing your readme should do is say what the project is.

00:05:48 And that's sometimes difficult for people to wrap their head around.

00:05:52 And it really gets at one of the fundamental problems of writing almost anything,

00:05:55 which is you have to decide who you're writing for.

00:05:58 And it's hard to know who might show up on your front page of your GitHub project.

00:06:02 And you don't know what they already know.

00:06:04 And so you don't know what you have to tell them.

00:06:06 So it's a little bit tricky to get all that information out there.

00:06:09 But for instance, under about here, it says the code coverage tool for Python,

00:06:13 which was the sort of pithiest, shortest description I could come up with to say,

00:06:18 what is coverage.py?

00:06:19 And I think that covers it pretty well.

00:06:21 I don't try to explain what code coverage is, because that's a topic you can Google for if you don't know what it is.

00:06:27 But so that covers it.

00:06:29 If you don't know what it is and you don't know you want it, you might not care about this.

00:06:32 So that's not your audience, right?

00:06:33 Right.

00:06:34 Why are you here if you don't?

00:06:35 Right.

00:06:36 Exactly.

00:06:36 But go ahead and start on your way out the door, please.

00:06:38 Thank you very much.

00:06:39 Right.

00:06:40 Exactly.

00:06:41 Yeah.

00:06:41 By the way, I could use a bunch more stars on coverage.py, because it's not a JavaScript project and it didn't start on GitHub.

00:06:47 So it's a little low on stars.

00:06:48 Yeah.

00:06:49 But so, yeah, the read me.

00:06:50 So I try to say what it is and then how to get started on it.

00:06:54 And I think those might be the front top two things.

00:06:57 I've got a thing there about Ukraine and badges, which we're going to get to.

00:07:00 But it's sort of there's the first paragraph there, coverage.py measures, code coverage,

00:07:04 typically during text execution.

00:07:06 So it tries to give sort of a little bit deeper explanation of it, what you can run it on, and then getting started.

00:07:12 There's a for enterprise thing there that links off to Tidelift.

00:07:15 But then the getting started tries to be very quick about, you just want to try it.

00:07:19 Here's some commands you can run to see how it works for you.

00:07:23 Because a lot of people, they just want to get going.

00:07:27 And if you can give them a quick instruction, then they'll be really happy.

00:07:30 Yeah.

00:07:31 Often four or five lines of code.

00:07:33 Here's how you use my thing.

00:07:34 Do I put a decorator onto a function and it does caching?

00:07:37 Do I await a database call?

00:07:40 Or like, what am I doing with this thing?

00:07:41 Right?

00:07:42 You don't have to be super complicated.

00:07:43 Right.

00:07:44 And sometimes it's not even clear.

00:07:45 Some people forget to mention, is this thing an application or is it a library?

00:07:50 Like just the big picture.

00:07:51 Like as a developer, you can be so, you know, in the trenches with your code.

00:07:56 You forget.

00:07:57 People don't know what it is yet.

00:07:59 Like what shape it takes.

00:08:01 Now, my readme is pretty short.

00:08:03 And actually the getting started doesn't show the commands.

00:08:05 It links to the getting start, the quick start section of the docs.

00:08:08 And the change history links to a separate part of the docs.

00:08:11 So it's actually a pretty short readme.

00:08:13 Some readmes can be very long, a little overwhelming.

00:08:16 You have to scroll past all the getting started to get to the change history.

00:08:19 For instance, I decided to take a different approach, which was to make it almost like a table of contents

00:08:26 to the places you might want to start in the larger docs.

00:08:29 That is a decision you have to make, right?

00:08:31 Do you try to put enough in there that it's basically standalone in a sense?

00:08:35 Or do you encourage folks to find their way over to a much more holistic sort of place, right?

00:08:42 That's an information architecture problem.

00:08:44 You know, the thing about writing a good readme is it's documentation.

00:08:48 And documentation has challenges all of its own that most developers haven't been trained in formally.

00:08:54 It's not really their first interest.

00:08:57 It involves thinking about other people, which let's just say some developers aren't skilled at.

00:09:03 But also the curse of knowledge, right?

00:09:04 Once you know what code coverage is, you don't feel the need to explain it or set the state.

00:09:10 You're just like, well, we want code coverage.

00:09:11 Of course you do.

00:09:12 And here's the tool, you know, for example.

00:09:14 Yeah.

00:09:14 So it's hard to decide what words to put in there, how much to say, how to organize it.

00:09:18 Those are all real challenges.

00:09:19 Well, it's quite popular with 7.5 million downloads a week.

00:09:23 Is that what it's up to?

00:09:24 Yeah, that's crazy.

00:09:25 That's what it says, right?

00:09:26 That's kind of insane, right?

00:09:28 And it supports all the versions of Python, even the fast one.

00:09:31 So that's cool.

00:09:33 Well, it's interesting.

00:09:33 So this is a point we might get to later.

00:09:35 So you're looking at the Python versions it supports on the badge.

00:09:39 Yes.

00:09:39 But if you actually read the text, it's actually mentioned, which goes up, the badge goes up to 3.11.

00:09:44 The text says it goes up to 3.12.

00:09:47 The alpha, yeah.

00:09:48 Alpha 2.

00:09:48 And that's because of how the badges work.

00:09:51 And there's reasons why people don't like badges because of that.

00:09:54 But badges look cool.

00:09:55 So you want the badges in.

00:09:57 What's going on here is that the badges show the status of the latest release on PyPI.

00:10:03 And so they're not in sync with what's in the repo.

00:10:07 And it's kind of a challenge to figure out what you want to do about that, unfortunately.

00:10:11 I do see, though, that you are a believer of badges.

00:10:13 You know, I kind of got into badges.

00:10:15 There's, what do we got on the screen here?

00:10:17 Six rows of badges, which honestly is a bit much.

00:10:20 And I should probably, I mean, it's just kind of a mosaic of green and blue at this point.

00:10:24 And it's kind of hard to get real.

00:10:26 But I'm kind of excited to see that you have a Mastodon badge.

00:10:28 The newest one.

00:10:30 I put a Mastodon badge on there, exactly.

00:10:32 Because that's the new crisis is moving from Twitter to Mastodon.

00:10:36 So I'm finding Mastodon to be a really nice place.

00:10:38 I mean, sort of sidebar for a second.

00:10:40 How are you thinking about this whole Twitter, Mastodon, open source community on social media thing?

00:10:45 Yeah, I'm looking at it as an opportunity to try out Mastodon.

00:10:48 And the thing that's really struck me about Mastodon is how many names of bloggers from 20 years ago I'm seeing again on Mastodon that I had lost track of.

00:10:59 And thinking like, oh yeah, I used to read that guy's blog 20 years ago.

00:11:03 And now we're connected on Mastodon.

00:11:05 And so we're kind of resetting back to a more distributed personal style of communication.

00:11:11 Twitter was great in that everyone was in one place.

00:11:16 So it was kind of easier to find people.

00:11:18 But Mastodon feels a little bit more like old internet.

00:11:20 Yeah.

00:11:21 It feels like open source social media.

00:11:23 I mean, and not just the fact that the underlying code is, but the philosophy of the federation and the different servers and the different smaller groups.

00:11:32 Right.

00:11:32 There's some downsides to it too.

00:11:33 You know, the server I'm on had some downtime while they were like rejiggering all their infrastructure because they suddenly had 30,000 users.

00:11:41 And all right, you know, I can do without, you know, Twitter slash Mastodon for six hours while they figure that out.

00:11:48 And then they're back and we're going.

00:11:50 Yeah.

00:11:50 I'm going to go for a walk or get some work done.

00:11:52 Yeah, exactly.

00:11:53 Awesome.

00:11:55 All right.

00:11:55 Well, that's a cool badge.

00:11:56 We'll come back to badges later.

00:11:58 I think that that sets the stage.

00:11:59 One more thing before we get into some of the tools.

00:12:03 There's places like, I think Tailwind CSS might land in this realm.

00:12:10 It's just too popular to search.

00:12:13 Let's see.

00:12:14 Just the Tailwind CSS, please.

00:12:16 Or I know Poetry.

00:12:18 I can't search for that alone, but Poetry with Python.

00:12:21 If you go to their websites, they've got like a fancy website.

00:12:25 Yes.

00:12:26 You know what I mean?

00:12:27 Yes.

00:12:27 And I see some open source projects like Vue.js maybe is like this, where it's almost like there's a marketing landing page for the project.

00:12:35 And the newer ones, of course, it is.

00:12:37 They'll have like a dark mode button.

00:12:39 And do you, how do you think about this?

00:12:42 When you see this, you're like, oh, I need to do this.

00:12:43 Or is this kind of.

00:12:45 I've never been tempted to build a page like this, partly because I don't think I have the skills to build a page like this.

00:12:50 And the things that I make are aimed at developers.

00:12:54 I mean, you're showing a Poetry page landing page here, which is also aimed at developers.

00:12:59 But I guess my feeling is developers don't need that kind of flash.

00:13:03 Yeah.

00:13:04 And honestly, if people use a different thing because it's flashier, that's okay.

00:13:09 I'm not out to corner the market.

00:13:11 Yeah.

00:13:11 It's not JavaScript code coverage.

00:13:12 It's not JavaScript.

00:13:14 That's right.

00:13:15 But also, I think sometimes it can be a little misleading.

00:13:18 And just to go back to Mastodon for a sec.

00:13:20 So one of the problems that people have with Mastodon is that they have to choose a server.

00:13:24 And that's the first choice they have to make.

00:13:26 And it's a difficult choice because it's an unfamiliar choice.

00:13:29 If you go to joinmastodon.org, it's a flashy site with cartoon elephants and things on it.

00:13:35 And it looks very easy.

00:13:37 But then the first button you have to pick presents you with a choice that's hard.

00:13:41 Here's your thousand choices.

00:13:42 Pick one.

00:13:44 Don't get it wrong.

00:13:44 It might have been less cognitive dissonance if the page looked a little bit harder so that when you got that choice, you knew what you were getting into.

00:13:53 It would kind of ease you into that hard choice.

00:13:55 Yeah.

00:13:55 I can see.

00:13:56 Actually, I hadn't looked at the page in the last few weeks.

00:13:57 They've actually changed it from choose a server to create account, which is good.

00:14:01 Yeah.

00:14:01 Because that feels more like what you're doing is creating an account rather than choosing a server.

00:14:04 But you click create account and you're on the page that says servers.

00:14:07 Yeah.

00:14:07 Oh, well.

00:14:09 They'll smooth that out.

00:14:10 They'll smooth that out.

00:14:11 You know, people used to be confused by Twitter.

00:14:13 We figured it out.

00:14:14 Yeah, I know.

00:14:15 But I agree that it's an interesting kind of marketing angle for software, which is a little bit weird.

00:14:22 Right.

00:14:22 But I should say, so coverage.py does have a mascot, which was drawn by my son.

00:14:29 Nice.

00:14:29 So it's got that cute aspect to it, but not the whole page isn't cute.

00:14:33 And actually, you're scrolling it on the screen.

00:14:35 I'm noticing the mascot isn't on the GitHub.

00:14:38 Should I go to the docs?

00:14:39 Page.

00:14:39 Yeah.

00:14:40 If you go to the docs, you'll see the mascot there in the upper left.

00:14:43 Very cute.

00:14:44 Sleepy snake.

00:14:44 Yeah.

00:14:45 So I've got a little bit of that, but that's because I've got a son who can draw like that.

00:14:49 And he made me a mascot.

00:14:51 If he hadn't done that, I wouldn't have anything cute on the-

00:14:54 Covered with a blanket.

00:14:54 Got it.

00:14:55 Yeah.

00:14:55 He's relaxing because he knows his tests are all covering his product and he's sleeping well.

00:15:05 This portion of Talk Python to Me is brought to you by the Local Maximum Podcast.

00:15:09 It's an interesting and technical podcast that dives into trends in technology, stats, and more.

00:15:14 But rather than tell you about it, let's hear from Max and Aaron about their show.

00:15:18 We are now on with Talk Python to Me.

00:15:22 Let's say hi to all the Python fans.

00:15:23 Hi, Python fans.

00:15:24 I'm Max Sklar.

00:15:26 I have actually done a lot with Python myself, so I am a fan of Talk Python.

00:15:30 Do you know Python, Aaron?

00:15:32 I took a course years ago, but I am a little rusty.

00:15:34 We are here today to talk about our podcast, The Local Maximum.

00:15:38 We've been on a roll lately with a new episode every week, and I wanted to share with you what

00:15:43 we've been up to.

00:15:44 Here on The Local Maximum, we tackle subjects in software and technology, topics as diverse

00:15:50 as the philosophy of probability to Elon Musk's next move.

00:15:54 For Talk Python listeners, I want to highlight a couple of recent episodes of The Local Maximum.

00:15:58 In 248, for example, I found out about an open source library that maps the world into hexagons.

00:16:05 And some pentagons.

00:16:06 I had a discussion with an author about games and puzzles, and another on a novel approach

00:16:10 to doing the job search well.

00:16:11 We discussed the ramifications of AI-generated art.

00:16:14 Have we reached peak creativity, or is this just another Local Maximum?

00:16:19 So check out The Local Maximum podcast available on your podcast app.

00:16:23 Okay, well, I think that's at the stage for this conversation pretty well.

00:16:28 Let's talk about ReadMe as a service.

00:16:30 Have you played with this any?

00:16:31 So I haven't played with this.

00:16:32 I tend to be very low tech in the way I approach things.

00:16:35 You know, edit some text files, build some tooling to make the result you want, and get

00:16:41 going.

00:16:41 So this looks like a good way to get started.

00:16:44 Like if you don't know what to do, this looks like a good on-ramp.

00:16:47 So it looks great.

00:16:49 If that's the way you like to approach things, definitely do it.

00:16:53 My philosophy is any way you can get a good ReadMe is a good way to get a good ReadMe.

00:16:58 So if this is going to help people, then I'm all for it.

00:17:02 It's not something you tie into your ReadMe.

00:17:03 It's a web app.

00:17:04 And it looks like one of these marketing page, landing page builders.

00:17:09 So on the left, it's got a bunch of different sections.

00:17:11 Like you can drag them in.

00:17:13 So you drag in the title and description.

00:17:15 You drag in the acknowledgements and fill it out.

00:17:18 And it will create the skeleton markdown.

00:17:20 And then you just take the markdown and run with it.

00:17:22 Right.

00:17:23 But it gives you a lot of structure.

00:17:24 Like, well, here's how a lot of people put their author acknowledgements.

00:17:27 Or here's how they put their example code or FAQ.

00:17:30 If this is...

00:17:32 So I haven't played with it.

00:17:33 But if the output of this is a markdown file that you then own and edit later on,

00:17:36 this is just a sort of a quick start templating thing.

00:17:39 I'm pretty sure that's how it works.

00:17:40 Yeah.

00:17:40 Any way to do it.

00:17:42 I'm personally always a little bit skeptical about new tools that I have to keep in my tool

00:17:48 chain and keep working and hope will remain maintained.

00:17:52 Personally, like low tech approaches.

00:17:54 Like I said, if you...

00:17:56 I have a text file that I can edit.

00:17:57 Great.

00:17:58 I'm all set.

00:17:58 So I like that this tool is a way to get started, but then gives you the text file that you then

00:18:04 own.

00:18:04 Yeah, exactly.

00:18:05 So when you're in a section, you just are working on these various pieces.

00:18:09 It kind of is like a function.

00:18:13 I'm just editing the internal, but it puts it all together in a whole thing and you get

00:18:17 just a raw markdown with a copy button.

00:18:19 And it seems pretty neat to me.

00:18:21 It is neat.

00:18:21 And because some of this stuff can be overwhelming.

00:18:24 I mean, markdown syntax is designed to be as straightforward as possible.

00:18:28 But once you get to badges, which are images with alt text with links, the syntax is no longer

00:18:34 simple and it's hard to remember how to do it.

00:18:36 So having a way to mash a button and have a badge show up on the page.

00:18:40 Great.

00:18:40 Let's do it.

00:18:41 So this was created by Catherine Olsner.

00:18:44 Olster?

00:18:45 Olsner.

00:18:45 And yeah, she works at GitHub.

00:18:47 So that's pretty cool.

00:18:49 But yeah, it's just basically a start from scratch and generate if you don't have a good

00:18:53 example.

00:18:53 So I kind of like that one.

00:18:54 Yeah.

00:18:55 And GitHub, in general, has one of their philosophies is we'll make on ramps for people

00:19:00 to do open source, right?

00:19:02 And like they've got in their documentation and their help, they've got how to use a console,

00:19:07 which isn't their problem to solve.

00:19:09 But they know that people are stuck getting into GitHub if they don't know how to use the

00:19:14 console.

00:19:14 So they're teaching people how to use the console.

00:19:16 They've got choosealicense.com because people don't know how to choose a license and they

00:19:19 need to in order to do open source well.

00:19:21 And so on and so forth.

00:19:22 So I love the on ramps that GitHub has built for these things.

00:19:24 Yeah.

00:19:25 And just the community as well, right?

00:19:28 You know, if you put your time and energy into this, there's a chance that people will

00:19:31 come along, appreciate what you've built and contribute to it as opposed to...

00:19:35 It's a social coding site.

00:19:36 That's their tagline.

00:19:37 Yeah, that definitely is.

00:19:38 They seem to be living up to it.

00:19:40 Okay.

00:19:40 Another one that comes from...

00:19:42 Yeah, this is the other end of the spectrum.

00:19:44 This is the other end.

00:19:45 There's a couple of other ones here.

00:19:47 This is from Hinnick.

00:19:49 This is your fancy project deserves a fancy pants readme based on Hatch or with Hatch.

00:19:56 Right.

00:19:57 Yeah.

00:19:57 So what do you know about this one?

00:19:58 Have you done anything with it?

00:19:59 I looked at this a bit and this looks like I said the other end of the spectrum.

00:20:02 So readme.so is kind of a visual graphical way to get started.

00:20:08 This thing by Hynick Slowak is a templating tool where you can automate the putting together

00:20:14 of your readme from different bits of information from all over your repo.

00:20:18 And it is a little bit overwhelming how much is there.

00:20:23 You look at the examples and you're editing .toml files with five dotted nested sections to get

00:20:31 the right pieces in place.

00:20:32 There we go.

00:20:33 And I totally understand this because I have built tools like this too where I thought,

00:20:36 you're a developer.

00:20:37 You can write me a regex when it comes time to tell me what to do.

00:20:41 So I totally understand this and I need to look more at it because it looks like it solves

00:20:45 some problems that I might be facing myself and my own.

00:20:49 Like if you look at the coverage.py repo, there's a lot of custom tooling to do these sorts of

00:20:53 things.

00:20:54 And if I can find other people's supported tools to do the right things, I would like to

00:21:00 use them.

00:21:00 I mean, like I said, I tend to spawn new side projects when I need tooling, but that's not

00:21:05 a scalable solution to things.

00:21:07 I should use other people's tools more.

00:21:10 They built AF, they built some good ones that are out there.

00:21:12 So here, let me see if I can find a section.

00:21:14 There's a little part.

00:21:15 That's it.

00:21:16 The impressive thing.

00:21:17 So when I first came to this, I thought I haven't heard of this Hatch Fancy PyPI readme

00:21:22 project, but under showcases, the black readme is built using this tool.

00:21:28 And that's fine credential right there that the black project is using it.

00:21:32 Yeah, absolutely.

00:21:33 And you've also...

00:21:34 As well as a bunch of others.

00:21:35 Yeah.

00:21:35 Structlog and JSON schema.

00:21:38 Yeah.

00:21:38 Yeah.

00:21:38 JSON schema.

00:21:39 Yeah.

00:21:39 Yeah.

00:21:39 So maybe I could read this one paragraph and this might give people the sense.

00:21:43 Do you want your PyPI readme to be the project readme, but without badges followed by the

00:21:48 license file and the changelog section only for the latest release?

00:21:51 Well, you've come to the right place.

00:21:53 So it's like...

00:21:54 He's got this whole assembly line model of there's already a bunch of information out

00:21:59 there.

00:21:59 So don't copy it around.

00:22:01 Don't try to write it in two places.

00:22:03 Instead, have a tool, pick up the information and then put it together into the readme, which

00:22:07 is what you want.

00:22:08 And I totally understand that because I've got some...

00:22:11 I've done some of that kind of tooling myself in my projects so that I can put a piece of

00:22:16 information in just one place and then it goes to where it has to go to be read.

00:22:19 It's a bit like a static site generator.

00:22:21 A bit.

00:22:22 A little bit.

00:22:22 The thing I still haven't wrapped my head around here is that what feels like it could

00:22:27 be one template.md file or something that says, you know, grab this from there and that

00:22:32 from there is instead in your PyProject.toml sections.

00:22:37 So you don't end up with sort of what looks like a readme.md file with callouts to where

00:22:43 the information should come from.

00:22:44 It's pieced together from the PyProject.toml sections.

00:22:48 I see.

00:22:48 The toml lets you reach into the different segments of the thing that's there.

00:22:53 Yeah.

00:22:53 And I understand why he's taking that approach because the PyProject.toml is there and this

00:22:58 is a hatch plugin.

00:22:59 So he's already got access to that information and it's bolted into the process of building

00:23:05 the distribution, which is the exact best time to build the readme.

00:23:09 So it's cool that he's explored it this way.

00:23:12 I have to take a deeper look at it to see if it would fit in with my workflow.

00:23:16 I don't use hatch.

00:23:17 Yeah.

00:23:17 Hatch is nice and hatchlane is nice.

00:23:20 And I've done a little bit of work with it.

00:23:23 And I can see why if you're already working in that mode, how to kind of extend it.

00:23:27 Absolutely.

00:23:28 Yeah.

00:23:28 One of the problems with coverage.py, which is my main side project is because it's 18

00:23:32 years old, there are bits of it that are using the latest, greatest technology as of 15 years

00:23:37 ago.

00:23:38 And because it's just kept working, you know, until it breaks, I'm not going to go and fiddle

00:23:43 with it or until I'm interested in fiddling with it, I might fiddle with it.

00:23:46 But there's a lot of stuff that's just old and weird and just keeps rattling along.

00:23:51 For such a highly used project, I can see the danger here.

00:23:54 But have you considered or have you run it through things like Flint to convert all the

00:23:59 strings to fstrings?

00:24:00 Have you or some of these like upgrade to the latest idioms where you can say, I want it to

00:24:04 be 3, 7 and above.

00:24:05 And anything that's older than that, you know, kind of rework it.

00:24:09 I have used pi upgrade on it when I dropped 2.7, which was a couple of years back.

00:24:14 And there are now fstrings all through it.

00:24:16 But for instance, I don't use black.

00:24:18 I there is a pull request to add type annotations to it.

00:24:22 But it's a big project that doesn't not gaining the momentum it needs to get done.

00:24:26 So I tend to, you know, let sleeping dogs lie where it's working.

00:24:31 And or if I don't, I don't know what I'm going to get out of it.

00:24:34 For instance, I use opt parse to parse the command line arguments.

00:24:38 And that wasn't even the right thing to use in 2.7.

00:24:41 That was the old thing that arg parse replaced.

00:24:44 But it still works.

00:24:46 It's still in there.

00:24:46 It's fine.

00:24:47 You know, sometimes there's no value in possibly adding bugs to something that you don't intend

00:24:53 to touch at all.

00:24:54 Right, right.

00:24:54 Exactly.

00:24:55 But maybe if you were to say, like, we're going to really dramatically expand the way

00:24:59 that it can take arguments and do things.

00:25:00 Well, then maybe all of a sudden you are like, we could get more flexibility with a new thing.

00:25:04 But if you're not going to touch it, then just let it be.

00:25:06 Yeah.

00:25:07 All right.

00:25:07 Let's get to the next one here.

00:25:08 Shields.io.

00:25:10 Yes.

00:25:11 If you want a badge, come to the place.

00:25:13 Shields.io, they will make a badge for you.

00:25:15 And this Shields.io is a very impressive service, I have to say, because they give you lots of

00:25:21 ways to make badges, including ways that I didn't even understand they could do.

00:25:26 I found this out when actually when I made that Mastodon badge that you can tell Shields.io

00:25:31 to go and grab some JSON from some other website and extract data from that JSON response and

00:25:37 include it in your badge.

00:25:39 So you just call the Mastodon API, public API to get stuff about your account and pull it.

00:25:45 If you look at my Mastodon badge, which is on GitHub slash Nedbat or on the coverage.py page,

00:25:51 it has my count of followers.

00:25:53 And that's coming from a JSON response from the Mastodon API on my server, on my Mastodon server.

00:26:00 And then Shields.io is incorporating that number into the image that it then serves to GitHub

00:26:06 to display into the readme. I don't want to think about how many computers are actually

00:26:10 involved to get that stupid number on that page. But it's very impressive that I can do all that.

00:26:14 I sure hope it's cash somewhere.

00:26:15 I hope so. I don't know.

00:26:18 How interesting.

00:26:19 Yeah, they've got a bunch of these prebuilt badges that can tell you all sorts of things.

00:26:22 Like, you know, what version of your project is current on PyPI and what Python versions it

00:26:29 supports and what your license is and all sorts of things. It's very impressive.

00:26:33 Yeah, it supports not just Python, but I saw Node.js, Nougat, PowerShell.

00:26:39 Yeah.

00:26:39 Stuff that I don't spend as much time on over here.

00:26:42 Yeah, there's things I've never even heard of that it shows here.

00:26:44 SourceForge.

00:26:44 They don't even document all the things it can do. I mentioned earlier that the badge on the

00:26:49 PyPI page will show the status of the latest PyPI release, which means if you go back 10 years to

00:26:56 the coverage.py, you know, version 3 release, there's a badge on it that shows you that it

00:27:01 supports Python 3.11 because the badge is showing you the most recent release, even though you're

00:27:05 looking at the badge on the 10-year-old release.

00:27:07 Yeah.

00:27:08 There's a syntax in Shields.io that will let you say, show me this factoids as of this particular

00:27:14 release 3.0.

00:27:16 I see.

00:27:16 And they don't document it, so I didn't realize I could do that. So there's an awful lot going

00:27:20 on in Shields.io.

00:27:21 Yeah. So if you want a Shield for one of those little badges for basically anything, these are,

00:27:26 you know, got downloads, users, test coverage, all these things. There's just a...

00:27:32 Right.

00:27:32 Basically, they give you a URL, right, that you put in into your readme, and that becomes the badge

00:27:39 as it resolves, right?

00:27:39 Right. The URL returns you an image with the information on it that you want. Either information

00:27:45 that you put into the URL, you can just make a URL that says, you know, Michael Kennedy is cool,

00:27:49 and it will return to you an image that says Michael Kennedy is cool. So, you know, it'll just format

00:27:55 things for you, but it also has ways of getting information and then formatting it to give back to

00:28:00 you.

00:28:00 Okay. You probably could put this personally onto places, not just on your project.

00:28:06 Right.

00:28:06 But maybe on your GitHub profile, potentially.

00:28:08 Absolutely. Yeah, my GitHub...

00:28:10 Like the social.

00:28:11 I'm embarrassed to talk about how over-automated my GitHub profile page is.

00:28:16 I love it. All right. Shields.io, that's a section for the live badges. This one is hot off

00:28:24 the presses. Let's see if we can find... Oh, it says initial commit. We got it 10 days ago.

00:28:30 Will McGuggan of Rich... Rich and Textual. And Textual, yeah. Put out a tool to generate a GitHub

00:28:37 flavored FAQ.markdown document. This is pretty neat. This is a tool. I just took a quick look at it. It's

00:28:45 in a similar vein that you want to make little bits of information in a convenient way and then have it

00:28:51 published as a monolithic piece of information. In this case, he's talking about FAQ questions. And I think

00:28:57 he said somewhere here, I got tired of answering the same questions over and over, so I made a tool

00:29:01 to make an FAQ or something like that. Yeah. I don't know. I don't have the same problem of needing

00:29:06 FAQs produced or why it's easier to put them all in separate little files that are combined together

00:29:11 later than just editing one big FAQ page. But Will's a smart guy. He must have had a problem and he solved

00:29:18 with this tool and it's cool to see. This is a little more similar to the way you described how

00:29:23 you might see building up the readme. Instead of defining an automo file, reaching into a giant

00:29:28 document, have a bunch of small ones to get assembled into a result here. Right. And that's a lot like some

00:29:34 of the change log management tools that we're going to get to also. Yeah. One of the things that prompted

00:29:40 Will to do this, he says here is people will ask the same question over and over and he in issues and

00:29:48 he's like, you know, I can't, I just can't answer it again. How to make a table. I mean, or can I make it?

00:29:53 So yes, you can make a table. Here's the link, whatever that is. So it has a fuzzy, fuzzy matching

00:30:00 on suggest. So I think this is why it's separate because you can put alias questions to the frequent

00:30:06 question. Yeah. And then you can just on the terminal on the shell, you can say factory suggest.

00:30:11 And if you have some kind of input to it, like I took the question that somebody asked me and I want

00:30:17 to point them at the thing so I can just jam that into the terminal and it'll go actually that matches

00:30:24 over to this FAQ response. I think that's the idea. And he says that it's designed to be used with a

00:30:30 GitHub action to post an automated response on an issue, I guess is the point is that if he's getting

00:30:36 a ton of issues that all need to be answered, instead of saying, go and read the FAQ, he can,

00:30:41 he's automated the process of putting the answer right onto the issue, which is cool. That's,

00:30:47 I didn't realize that aspect of it. So that's very cool. So this is all of 10 days old. People can

00:30:51 check that out if they want. Hot off the presses, torn from today's headlines. Exactly.

00:30:59 This portion of Talk Python To Me is brought to you by Sentry. How would you like to remove a little

00:31:05 stress from your life? Do you worry that users may be encountering errors, slowdowns, or crashes with

00:31:11 your app right now? Would you even know it until they sent you that support email? How much better

00:31:16 would it be to have the error or performance details immediately sent to you, including the call stack

00:31:21 and values of local variables and the active user recorded in the report? With Sentry, this is not only

00:31:27 possible. It's simple. In fact, we use Sentry on all the Talk Python web properties. We've actually fixed a bug

00:31:34 triggered by a user and had the upgrade ready to roll out as we got the support email. That was a great email

00:31:40 to write back. Hey, we already saw your error and have already rolled out the fix. Imagine their surprise.

00:31:46 Surprise and delight your users. Create your Sentry account at talkpython.fm/sentry. And if you sign up with

00:31:53 the code talkpython, all one word, it's good for two free months of Sentry's business plan, which will give

00:32:00 you up to 20 times as many monthly events as well as other features. Create better software, delight your

00:32:06 users, and support the podcast. Visit talkpython.fm/sentry and use the coupon code talkpython.

00:32:16 We talked about contributions and how people appreciate getting credit for participating.

00:32:22 You know, like I'm sure there are people who have closed a small issue or found and fixed a small bug

00:32:28 in coverage.py or added a small feature and feel really proud of that, right? But yeah, they would

00:32:33 feel more proud if you acknowledged that they did it, right? I accept your PR, right? Of course.

00:32:38 So tell us about this all contributors place here. This is a GitHub bot that on an issue,

00:32:45 you can say, you know, add all contributors, add Michael Kennedy to the bug fix sections of the

00:32:52 contributors because he did it right here in this issue that we're talking about. And that's really

00:32:57 cool because I don't use this tool. Like I said, I tend to be very low tech. I do acknowledge my

00:33:02 contributors. I'll mention them in the changelog. And I have a contributors.txt file that lists everyone

00:33:07 who's contributed in some way. And I will hand edit that. And it can be, you know, I have to remember

00:33:12 to put it over there and put it over there. I don't get so many contributions to coverage.py that it's

00:33:18 a burden. And I kind of actually like that little sort of moment of zen of, you know, finishing the

00:33:23 paperwork and crossing the T and dotting the I's. But if you're on a big project where you are getting

00:33:28 a lot of contributions, I could see how doing this with a bot would be, you know, save you that little

00:33:33 bit of work that that could become a big amount of work. And you don't want to skip it, right?

00:33:39 Because like we said, it's seems like a small thing to us and maybe like, I don't want to have

00:33:43 to bother. But it's a huge thing to the contributor to have their name mentioned.

00:33:47 Yes. Yeah.

00:33:47 And maybe not just pride. Maybe they get a job because of it. Right. They could say,

00:33:51 I'm getting hired to work on Flask. Look here. I'm listed as a contributor on Flask.

00:33:56 That puts me above 99% of the other people applying.

00:33:59 That's right.

00:33:59 At least in that regard.

00:34:00 The internet is the kind of place where you don't, when you're, you get a little connection

00:34:04 like that, you never know what it's going to lead to.

00:34:06 Yes.

00:34:06 There's all sorts of things that pop up because of the strangest little mentions.

00:34:10 So true.

00:34:11 You might get invited to be on a podcast just because someone mentioned one of your dopey

00:34:15 little tools on Mastodon.

00:34:17 Or you might even start a podcast.

00:34:19 You might even start a podcast. Yeah. Watch out.

00:34:21 That's right.

00:34:22 There's danger ahead.

00:34:22 And then you're really in for it. So the way that this allcontributors.org bot seems to work,

00:34:28 I don't use it personally because I don't have projects that are big enough to really

00:34:31 justify this in terms of open source projects. But in the comment on an issue or on a PR or

00:34:37 one of those types of things, you can just say at all contributors, please, please add at

00:34:43 GitHub name of contributor. And then it says for design or for bug fixes or for documentation.

00:34:48 And then the dot, the dot, the bot says added them as contributor. That's, that's really cool.

00:34:54 Yeah. So I, like I said, I have a text file. One of the, one of the unusual things I do with my text

00:34:58 file is that when I build for coverage.py, when I build the release, if you go and look at who,

00:35:04 who the author of coverage.py is, it says Ned Batchelder and 137 other people. And that number,

00:35:11 137 is counting the number of lines in the contributors.txt. Cause I want it to be clear

00:35:16 that, yeah, it's not just me. There's lots of people helping with this and you can help too.

00:35:20 Yeah. Especially over 18 years.

00:35:22 Well, yeah.

00:35:23 All right. Getting to the part of expanding beyond just readme.md, but the broader

00:35:28 experience of things that maybe gets, gets their way pulled back into the readme is a changelog.

00:35:35 Yes.

00:35:36 Are you familiar with keepachangelog.com? Have you seen this?

00:35:39 I am very familiar with keepachangelog.com.

00:35:41 All right. Tell people about this.

00:35:42 So keepachangelog is basically an advocacy site that says you should really have a changelog. And

00:35:47 here's what we mean by that. And why should you do it? And I absolutely agree with the idea

00:35:53 of keeping a changelog, which is a running history of what has changed in your project.

00:35:58 And that's because people that your users want to know what's changed. I mean, it sounds really

00:36:04 simple, really basic, but I think people can approach it in really simple ways that aren't

00:36:10 as valuable. And if you put a little bit more work into it, you'll find it's really, really valuable.

00:36:15 And you need to know as a consumer of a library, is there an immediacy to this new version that I

00:36:22 need to pay attention to? Is there a risk to this new version that I should be aware of?

00:36:26 Or do I don't care? And I just leave my thing pinned the way it was before, right? If it says

00:36:29 there is a CVE where if we send the dollar sign, it takes over your server, like you should get in

00:36:35 there straight away.

00:36:36 Yes, exactly.

00:36:37 Exactly.

00:36:38 But if it says we deprecated this thing that you were depending upon, like, well, don't just push it.

00:36:43 We're going to need to think about this.

00:36:44 Right. And I think the way you just described that is really good, which is that the user of the tool,

00:36:49 the library, the application, they want to understand, you know, what's in it for me?

00:36:53 Like from my perspective, what has gone on with this library? And I think that's one of the things

00:36:58 that's difficult for people is for maintainers is to put themselves in their user's shoes and think,

00:37:04 what's changed about this that matters?

00:37:07 Yeah.

00:37:07 There are some auto-generated changelogs that, for instance, just put all the git commit messages

00:37:11 in the changelog. And those drive me nuts because they're telling me all sorts of things that I don't

00:37:16 care about. I don't care that you restyled, changed all the spaces to tabs in some file.

00:37:22 That doesn't matter to me. That's just noise. You're hiding, you're burying the lead by telling

00:37:27 me stuff that doesn't matter. So keep a changelog is a good, like I said, advocacy site. They have

00:37:33 their guiding principles. Change logs are for humans, not machines, things like that. And they

00:37:37 advocate for marking your commits with, or marking your changelogs, putting them into sections of what's

00:37:44 been added, what's been changed, what's been deprecated so that, you know, people can zero in on what

00:37:49 matters, right? Deprecated means I can't use the thing anymore and I need to make a change. And security

00:37:54 means I really better get on this or I might be in trouble. So it's good to highlight those things and

00:37:59 put it into the user's perspective. But I like the guiding principles here about it's

00:38:03 for humans. Every version should have one. The release date should be specified. It's easy to

00:38:09 just say, well, version 2.1 had these changes. Like, well, wait a minute. We're on three. Like,

00:38:14 was that last week or five years ago? I need to know how relevant.

00:38:18 Date things. I mentioned my son doing art. I always told him when he was a kid, put the date on the

00:38:23 picture. So I'll know how old you were when you made the picture and you never wanted to do it.

00:38:26 But change logs, you can put dates on things. Like you said, you don't know how long ago something

00:38:31 was. Yeah. Don't have to go back and diff the thing to figure out when it was committed. Right. All

00:38:36 right. And we've got one chat from a viewer talking about creating change logs, like as a good job for

00:38:42 AI. And these days, I don't know, 2022, not only is, you know, Twitter versus Mastodon, but chat GP,

00:38:49 what's it called? The AI thing? GP3, I think. Yeah. Something like that. Seems to be amazing.

00:38:54 And I can probably retire soon because it's going to do my job, I think. Yeah. And just yell commands,

00:39:00 just yell stuff at the computer from like the couch. Computer, go write the website. Just make it

00:39:05 better. Scale the website, computer. Exactly. Oh yeah. That's a good point. Mario out there says it's

00:39:12 called Skynet. There are some amazing tools, like a bit of a diversion, but there's like this thing

00:39:17 called Jasper that a friend just told me about. And what you do is you write, it's like Google

00:39:22 Copilot for writing content. And there's just, there's a bunch of crazy, crazy things out there.

00:39:28 Yeah. It is. We've seen a complete change in the progression of things and it's astounding.

00:39:34 It is. All right. Well, let's get to one of the first tools that got you recommended. The reason

00:39:39 I invited you is because I asked people for general recommendations and they kept recommending your

00:39:44 tools. I'm like, all right, well, I should just have Ned come on the show to talk about this.

00:39:47 I'll just come in and talk about all of it. Sure. All right. So we, we saw the, keep a change log

00:39:52 ideas, but that's in theory, not in practice, right? Right. To keep a change log just says,

00:39:57 look, you should write this stuff and here's how you should write it. It's not a tool.

00:40:00 It's just encouraging people to do a good job. I looked around at tools when I wanted to get

00:40:05 people to make better change logs. And there was one called town crier from the twisted project.

00:40:11 And they solved the problem that a lot of change logs have. So if you just have a change log file

00:40:16 and everyone who makes a change to the code is supposed to put an entry into the change log file,

00:40:20 then that file becomes a merge conflict every time, right? Because I added a feature. I put my thing at

00:40:25 the top. You added a feature. You put a thing at the top and it's a merge conflict. Years ago at work,

00:40:29 what I tried to do is have a change log file. And I told developers, put your change near the top of

00:40:34 the file in the hopes that they wouldn't merge conflict. And developers would come to me and say,

00:40:39 what do you mean by near the top of the file? Because they're engineers, they need precise directions,

00:40:43 right? So, okay, that wasn't going to work. So the idea that town crier uses, and also the cpython

00:40:49 source code has a thing called blurb that does the same idea, which is when you make a change to the code,

00:40:54 you also write one small file, which has just the entry for the change log in it. And you check that

00:40:59 in. There's a special directory that just has those little fragments in it. And so when you make your

00:41:04 code change, you also add a fragment to that directory. And then later, when it's time to actually

00:41:09 put everything, you know, make a release, all those fragments can be concatenated together to become

00:41:14 the change log. And the good thing about that is that you don't have merge conflicts because everyone

00:41:19 creates their own fragment. They have, you know, unique names based on some principle. And then at

00:41:24 publication time, you know, when the release is made, they can get concatenated together. And like

00:41:29 I said, town crier did this and blurb also did this. I looked at them and they were both a bit more

00:41:34 opinionated than I wanted. I knew that if I was going to get a lot of people to use this thing, that it

00:41:41 needed to be very, very flexible. And I actually took an approach when I was building Scriv of what's the

00:41:46 least opinionated I can be. How many different ways can I let you decide how you want it to work?

00:41:50 At the time, black was rising in its popularity and it was famously opinionated. And so I sort of took

00:41:57 the opposite approach. Nice. Scriv's, the idea is that it's got a few commands. You say Scriv create

00:42:02 to make a fragment, Scriv collect to collect them all together. Those are the two main ones.

00:42:07 Scriv looks like, it looks like a great tool. And it looks like one of these things you could pipx

00:42:12 install because you're not going to, it's unlikely you'll depend upon it for your code to run.

00:42:17 You just need that command around to manage a project.

00:42:20 Right. Or you can put it into your development requirements.txt or however it is you manage

00:42:25 your project tooling. But sure, pipx would work too. And it's actually grown one other command

00:42:31 for making GitHub releases. So it will actually parse your changelog file. Even if your changelog

00:42:37 file wasn't made by Scriv, it will parse your changelog file and then create a GitHub release

00:42:42 from your changelog file, which gets at a philosophical opinionated point of mine, which is that

00:42:48 the information should live in just one place. And that place should be a file that you check

00:42:53 into Git. It should be a file that people can clone when they clone your repo. If they want

00:42:57 to just look at the changelog in Emacs or whatever locally, they should be able to do that. And since

00:43:02 you don't want to duplicate information, but people do seem to like having GitHub releases

00:43:07 make, you know, publish a GitHub release based on the information from the changelog file,

00:43:11 rather than having the release be the source of truth where it can't be cloned. It can't be

00:43:16 edited. It can't be, you know, there's no commits that you can track to see who put that text there,

00:43:21 those sorts of things.

00:43:22 Okay. And that makes a lot of sense. Let's see. Out in the audience, we got in a question.

00:43:26 Last changelog I read was for Python 3.11. Did you read that? Have you read? It's a bit of a novel.

00:43:32 The CPython developers have taken to heart the idea. And I make it sound like this is a recent

00:43:37 development. They've always done this. You know, there's a Python 3.11 has a what's new in 3.11.

00:43:42 And they tend to be very, very detailed about putting stuff in the what's new document. And like

00:43:47 I said, they've got their own custom tool called Blurb, which is how CPython core developers,

00:43:53 they write what are called news entries, which get created as small files in a custom,

00:43:57 in a dedicated directory. And then those get aggregated into the what's new document.

00:44:02 In that changelog, there's 180,000 words. Typical novel is like 80,000. So that's a proper changelog

00:44:10 right there.

00:44:10 There's more information there than any one person needs, but everything that's there,

00:44:15 someone does need.

00:44:16 That's right.

00:44:17 Right.

00:44:17 And each one of those links to like a GitHub issue or a PEP or something like that.

00:44:22 Yeah.

00:44:22 And there's a lot of those. I just noticed, I think it was today that they got GitHub

00:44:26 issued number 100,000 in the CPython.

00:44:29 Wow. Okay. That's major.

00:44:30 Yeah.

00:44:31 It's been chugging along for a while. All right. So this looks like a great idea. What do we

00:44:34 got up next? Oh, I just also wanted to just give credit, speaking of giving credit from

00:44:38 Colin Sullivan, who sent this in amongst some other things as well over on Mastodon. So thanks

00:44:44 for sharing that. This is another one. I'm going to go quick because it's not a Python

00:44:48 tool and it's actually in a technology I've never heard of. Maybe you've heard of it, Ned.

00:44:52 So I hadn't heard of this. So this is called Changelog Manager from Masukomi. And it's

00:44:57 interesting that he, Masukomi, is one of those bloggers from 15 or 20 years ago that I'd lost

00:45:03 track of and suddenly got reconnected to on Mastodon. And when I asked about, I got a little

00:45:09 petulant on Mastodon about a changelog that I found completely useless. And he chimed in

00:45:14 with a long thread about how aggravated he is by changelogs and how hard it is to get people

00:45:19 to do them well and pointed me at this tool that he had written about.

00:45:22 It looks like a cool tool. People can check it out if it works well. It's written in a language

00:45:27 called or technology called Crystal. I feel.

00:45:29 Yeah. I don't know what that is.

00:45:31 Makes me feel old all of a sudden not even know that that's a language. I don't know. But wait,

00:45:36 hey, look, it's Colin's out in the audience. Oh, hey, Colin. Yeah.

00:45:41 Thanks for the recommendation. You got me on here.

00:45:44 Yeah, absolutely. So this is a cool project here and people can check it out. And yeah,

00:45:49 it's got a lot of the philosophy of how you should do it, how you shouldn't just have

00:45:53 commit messages. I remember hearing about tools that would look for swearing and other kinds of

00:46:01 frustration in commit messages and not allow those particular messages to get into the changelog.

00:46:07 But I don't think that, as you pointed out already, that individual commits are generally

00:46:12 the right granularity.

00:46:13 Right. Commits definitely are not. Some of these tools will aggregate your pull requests

00:46:17 to be the changelogs. And that's a little bit better because they're larger grained. But even so,

00:46:23 I think there's real value in hand curating your changelog. Start with a list of pull requests,

00:46:30 but then take a look at it, reorder them so they make some sense and tell the story.

00:46:34 Right. Put the important stuff on top.

00:46:35 Put the important stuff on top. If you have three pull requests, which just by coincidence all changed

00:46:40 how you handle file matching, then make an entry that says, we changed a bunch of things about file

00:46:46 matching and then have sub bullets about the file matching changes. You want to explain things to

00:46:51 people and you're going to be able to do a better job of it than your pull requests or your commit

00:46:55 messages. Absolutely. All right. Well, thanks for that, Colin.

00:46:57 Executable books. The executable books folks are interesting. They've got a lot of tools that will

00:47:03 take Jupyter Notebooks and other things using the MIS plugin for markdown and generate books in

00:47:11 different ways. And so they've got this project called GitHub Activity, which generates a simple

00:47:16 markdown changelog based on that. Let's see. I think this is on issues and PRs, not commits.

00:47:25 Yeah. I think this is one of the ones that goes for the larger chunked bits of information,

00:47:30 which like I said, is good. Commits are too small. The issue is still that when you write a pull

00:47:37 request, what you're writing about mostly is something that your reviewer needs to read.

00:47:41 Right. So you're really addressing your collaborators rather than your users. I mean,

00:47:46 ideally your pull request would include all of the user consequences as well, but it's also going to

00:47:52 talk about what your collaborators need to know. So different audiences, different information at the,

00:47:57 at the very least, it's going to need an editing pass in order to figure out how to actually explain

00:48:02 this to people the right way.

00:48:03 Sure. Well, that's an interesting idea. Maybe the tools don't have to be perfect. Maybe they could say,

00:48:09 well, here are the 10 things in terms of PRs and issues that have changed. Now just rewrite that for

00:48:14 humans with a different audience. That still could be valuable.

00:48:17 Yeah. Collecting up all the information. That's great. I just think it needs, it needs a human

00:48:21 touch.

00:48:21 Yes.

00:48:22 That's controversial in these days of AI, but I think humans can do a good job writing stuff.

00:48:26 Indeed. As we say, get up co-pilot, write me a, no. So the next one we come to is Dinghi?

00:48:34 Dinghy.

00:48:35 Dinghy. Okay. Dinghy. Got it. Just like the little boat thing.

00:48:37 The little boat. That's right.

00:48:38 Okay.

00:48:39 Yeah. So this is a tool that I wrote and it was interesting because when Colin mentioned this

00:48:42 as a tool for changelogs, it didn't, that's not why I wrote Dinghy. Dinghy is designed to give you a

00:48:48 daily digest of GitHub activity, which by the way is why it's called Dinghy because the D-I

00:48:53 stands for digest and there's a G-H in it, which stands for GitHub. And I looked through words that

00:48:58 had those pairs in them and Dinghy popped out.

00:49:00 Nice. And it's got a Y, which is like half a Python for pies.

00:49:03 And it's got, yeah. And then you can, you can backfill the marketing slogan of, you know,

00:49:07 your lifeboat on a sea of information or something like that.

00:49:10 There you go.

00:49:11 Dinghy just gives you a digest of your GitHub activity. I was finding at work that I had to

00:49:16 track lots of issues and pull requests and there were lots of repos where I wanted to know what

00:49:20 was going on. And so I found it useful to just summarize the activity on issues and pull requests

00:49:26 across repos.

00:49:27 This is nice.

00:49:27 Yeah. In the morning, take a look what happened on the last day. Oh, I should, you know, I should dive

00:49:32 deeper into that one. I can click into it and go read the real issue, but you just can get a,

00:49:36 get a quick overview, but I can see how, so I use it sort of on a daily basis, but I could see how

00:49:41 you could take this and get a digest of the last three months and then use that as at least a guide

00:49:48 to where to get the information for a change log. If not, you know, pulling information right off.

00:49:52 It seems real helpful if you work on a team, especially if you're the team lead or kind of a

00:49:56 manager type and you're like, all right, just need to see what's happened on these three projects

00:50:00 this week. Exactly. Just hit it.

00:50:02 That's what it's for. And it's, it's satisfying to hear people think of other uses for it. That's

00:50:06 the sign of having built a useful tool is that I meant it for one thing, but then someone else

00:50:12 sees, oh, I could use it for that too. And that's very gratifying.

00:50:15 I can see it at the end of a sprint, like the sort of post-mortem burn down type of thing.

00:50:19 Yep.

00:50:20 Yeah. Okay. Cool. Cool.

00:50:21 You mentioned blurb. I'll just put a link to, to the blurb project tool as well. This is the

00:50:27 CPython prolific writer. This idea of building the change log from small fragments is something

00:50:35 that's happened a number of times. And I think it's a great idea. I think it's the right way to,

00:50:39 to do this kind of work. Agreed. One that comes, I, is this GitHub itself that does this? No,

00:50:45 there's not. There's a thing called release drafter and it drafts your next release notes

00:50:51 as PRs are merged into a master. Okay. So I haven't used this.

00:50:55 This is another case of things going into GitHub actions. And I'm fascinated by this whole thing,

00:51:00 you know, as a project maintainer, I feel like there's sort of three large buckets of work.

00:51:05 There's the building, the product itself. I don't mean product to sell, but like coverage.py is a

00:51:10 product. There's maintaining the test suite for it, which is if you've got a large test suite is a

00:51:14 whole endeavor all to itself. There's all this project automation, you know, that we've been

00:51:19 talking about here today. You know, how do I get the releases made? I've got a make file,

00:51:23 what this command, how do I, what's, how do I bump the version up? Like all of that kind of,

00:51:27 and it feels like micro automation. You're doing it like one shell command at a time or a 10 little

00:51:31 Python, 10 line Python file or something. And the fact that there are all these tools around

00:51:35 that help with it and put it in GitHub actions. And you just, you make a GitHub,

00:51:39 a Git tag and suddenly it goes to PyPI and publishes the GitHub release and all that.

00:51:45 That's fascinating to me how far you can automate those processes.

00:51:48 They kind of build up like a snowball going downhill pretty quick because you're like,

00:51:51 well, if I could automate this thing and that thing, they're like, wait a minute. Now we just,

00:51:55 they click together and then it's, we're almost there.

00:51:59 I'm a late adopter of technology. I won't automate a thing until I know that it's exactly the way I

00:52:04 want it. And I've gotten completely sick of doing it by hand. But the good news is by then I do know

00:52:09 exactly what I want it to do. And so I can build the automation and I don't have to come back and

00:52:13 fiddle with it too much. Another big benefit I would say to that approach is every time it runs,

00:52:18 it could just warm your heart with a joy. Like I, you know what, I hold another two hours. I didn't do

00:52:23 that thing. That's right. The downside is when it does the wrong thing. So this weekend,

00:52:28 I actually had a big weekend this weekend. I released 1.0 of both Scriv and Dingy and the

00:52:33 first beta of coverage 7.0. And it turns out that the links to PyPI on the readme, no, the links to

00:52:41 my documentation from the PyPI readme are broken because they don't work if it's a beta release.

00:52:46 And I didn't know that until the release was published and betas happen so infrequently,

00:52:51 it'll change again before I make another one. And it'll probably be broken too, because it's hard to

00:52:56 test this kind of automation. Like the good thing about building the product and building your test

00:53:01 suite for the product is that that is automation. You can run the crank on and you know if it's

00:53:05 working or not. Releasing projects, if you build automation for that, how do you test that if release

00:53:11 happened correctly other than actually making a release and then getting bug reports from people

00:53:16 about the 404s on your PyPI page, which is how I found out about this. It's a little frustrating.

00:53:20 For as much fantastic testing software and automation, sometimes you just got to hold your breath and

00:53:28 push the button. And you're not going to write a unit test that says, let's push this thing to

00:53:32 test.pypi.org and see if all the links on the readme are right. That's, I mean, maybe, I guess you could,

00:53:39 but if anyone's done that, please get in touch because I messed that up this weekend.

00:53:44 At some point you got to go, okay, we've tested enough. It's got to go. And even if you write a

00:53:49 unit test, you know, it's not necessarily exactly the same. It's not the same and you'll fiddle with

00:53:54 it and break it. And which is what happened to me. And yeah, absolutely. There'll be another release.

00:54:00 It's fine. There'll be another release. We'll get it fixed. All right. You mentioned Town Crier

00:54:04 already. I think maybe we can just carry on, but people can check that out as well. You know,

00:54:09 I guess give them a quick shout out as well while we're here. This comes from the Twisted project,

00:54:12 you said? Yeah. And Twisted is another of these projects that's been going for a very long time.

00:54:16 So this is a mature tool. It's just a little bit quirky in the way that they wanted to do things.

00:54:22 I think at least when I first looked at it, it was something like the fixes went into a .fix file

00:54:27 and the features went into a .feature file, things like that, which just, and it didn't do markdown.

00:54:32 And I knew that I was going to have people who needed markdown, even though I prefer

00:54:36 restructured text. So I built Scriv to kind of along the same ideas, but in a more flexible way.

00:54:43 Right. Okay. Cool. One of the things you may have in your readme or other parts of your documentation,

00:54:51 your markdown files or restructured text, I suppose, would be example code. Like I talked about that.

00:54:56 It would be nice to know some level of correctness to that, right?

00:55:01 Yes.

00:55:02 We have MKTestDocs. Tell us about this.

00:55:05 This is one of these things that's the interesting thing to me is that you've got docs, you've got tests,

00:55:09 you've got doc strings, and there's all these tools that do all the different pairings of stuff,

00:55:15 right? So you can run tests against the code in your doc strings. This runs pytest against markdown

00:55:22 files that have code in them. So it's running the code in the markdown files. And it's fascinating,

00:55:27 again, to see how all of this automation, this project level automation comes together to try to

00:55:33 close all those little gaps. Like I mentioned the problem of a broken URL on my readme. You could

00:55:38 also have code that you had typed into a markdown file, and it turns out it doesn't work for whatever

00:55:43 reason. Maybe it worked once, something changed. This will run the code in your markdown files so that

00:55:49 you know that it still works, which is great. I'm all for more testing.

00:55:52 Yeah. Well, even if you're not actually trying to execute it, and like I'm asserting that my example

00:55:58 returns seven, because maybe it says connect to a database and do other crazy stuff, it could at least

00:56:03 be syntactically valid.

00:56:05 Yes.

00:56:05 Right. It could look at it and go, I loaded that up and I parsed that function and it didn't die.

00:56:09 That's a start.

00:56:10 Exactly. There's levels of testing. And like you said, it can get very complicated to do full testing of

00:56:16 some kinds of code.

00:56:18 So how do you test your markdown, your readme.md? Well, see, I fire up a series of a cluster of Docker

00:56:25 containers using Docker Compose, and then we can run the one example and then it's good.

00:56:29 If there's a tool out there that launches missiles, I don't want to know how you're testing the code

00:56:33 in your readme.

00:56:34 Yeah. There's another one that is a little bit tough to test. One of the things that's interesting,

00:56:39 by the way, this tool comes from Vincent WormerDem, that it deals with multiple code blocks. So if you

00:56:46 do the language specifier in markdown, so the triple dot back tick, and then you just say the word

00:56:52 Python or JavaScript or C# or whatever, that'll tell the formatters, format it like,

00:56:59 this, right? It's this type of syntax you should see. So if you do the Python one,

00:57:04 it will run those. And it'll also do bash as well, I believe. But what's interesting is you could have

00:57:10 a, like, and here's how you set it up, and then here's how you call it type of series of code blocks.

00:57:15 And it will run all the code blocks, or you can actually say, you know, remember what you saw

00:57:21 before, because that was the first half of what you need to do the second half.

00:57:24 Right. Because you're trying to tell a story. This is like a Jupyter notebook where you're

00:57:27 interspersing code with commentary and then more code, and you need the multiple blocks of code to

00:57:34 all be executed together, or, you know, one after the other. You need the first one's results in the

00:57:39 second one.

00:57:39 I certainly appreciate a don't completely repeat yourself every time in your code example,

00:57:45 right? It would say you get started by importing this, and then you would create a class like this

00:57:49 that it arrives from. You wouldn't want to have to have import, import, import over and over,

00:57:54 right? So yeah, this is cool. I don't use this one either, but it definitely looks like something I

00:57:58 could see adopting. Now here's something called shed, which is not exactly what I want to talk about,

00:58:06 but it's for formatting code. So it runs autoflake, it runs pyupgrade. You mentioned that before,

00:58:11 I believe, for upgrade. You can specify a version, pyupgrade me to Python 3.8, but not further,

00:58:17 please.

00:58:17 Pyupgrade is good.

00:58:18 Yeah. Yeah. It runs black. But what I do want to talk about is it runs black in docs.

00:58:23 Which formats the code in the doc strings and in your docs. Which again, is one of those pairings of,

00:58:30 let's put this tool into that thing and have it do just a little bit.

00:58:35 This is super hard to get just right because you want to format code. And, you know, one of my

00:58:41 markdown editors, if I highlight some code and I hit shift tab to unindent, it'll put everything just to

00:58:47 the left. I'm like, no, no, no, no, this is Python code. It has to have the space. You can't just put

00:58:51 it all the left, like undo one level, right? The things like that, where it's just like, oh, this,

00:58:55 this is not quite formatted, right? Just running this maybe even as a pre commit hook would be

00:59:02 glorious. Just like all of my code in my examples and my triple back tick Python becomes black,

00:59:08 blackened.

00:59:09 Yep. And if you're using black, then you really want it everywhere, right? You've given up control

00:59:15 of the formatting of your code willingly. You see the value of it and you just want it everywhere.

00:59:21 And this is great for getting it into your docs too.

00:59:23 Exactly. Like there's, there's gaps. Maybe your Jupyter notebooks don't have black formatter,

00:59:27 like get it in there, get it into the docs, get it everywhere.

00:59:29 Yeah. Getting to read me. Cool. Okay. let's see this one. Another person gave a shout out to

00:59:36 your next project here. This is Cy Gallimardi said, Hey, we should check out cog.

00:59:42 Yeah. Cog is one of those tools that I wrote very long time ago to do one particular thing.

00:59:48 And it ended up being useful in lots of other ways. Basically cog is a way that you can make a text file

00:59:55 like a readme.md and put little bits of Python in the middle of it. Not because you're trying to

01:00:00 display that code to people, but because you want the results of that code to be part of your document.

01:00:05 A little bit like a, a Jinja, right? A template maybe.

01:00:08 Exactly. But it's a little bit backwards because Jinja starts with the idea. I mean,

01:00:12 Jinja is, well, it is like Jinja actually. I should, I shouldn't say that. It's just like Jinja.

01:00:16 But instead of being HTML, you want it to be text or something, right?

01:00:19 Right. It can be anything you want. Jinja is particular to HTML in some ways,

01:00:23 but cog is completely agnostic. The bigger difference from Jinja with cog is that the output of your code

01:00:30 can go into the document so that you process, you run the document, the output of your code

01:00:36 becomes part of the document. So sort of the input file and the output file are the same file so that

01:00:41 you get sort of an item potent kind of processing of the file. So you can have a readme.md. You run cog

01:00:47 on it. You still just have a readme.md, but now you've got the results of the computation in the file.

01:00:52 So for instance, I use this in the coverage.py docs. There's a database schema for the SQLite data

01:00:58 file that coverage.py writes. That schema is in a string in a Python file someplace, but I also want

01:01:04 it to be in my docs. So I use cog in the restructured text file to go and get the string from the Python

01:01:10 code and splat it into the restructured text file so that I know that the two are the same because

01:01:17 there's one source of truth and an automated process to bring it into the restructured text file.

01:01:22 You know how they say there's like two hard problems in computer science, naming things,

01:01:26 caching validation and off by one errors. Yes. I feel like maybe a fourth one should be

01:01:31 identifying and controlling and keeping the one source of truth.

01:01:35 One source of truth is a big thing with me and all of these kinds of processes where

01:01:40 you want to make it convenient to write information, but you also want to make it convenient to read

01:01:46 information. And so you might want to publish information in more than one place. For instance,

01:01:50 I mentioned that my changelog is in a .rst file, but it also goes into GitHub releases because people

01:01:57 want to read it in GitHub releases. So I get the information out of the changelog and automatically

01:02:02 publish it into GitHub releases. Yeah.

01:02:04 Cog has found a lot of use. Simon Willison has been very positive about Cog. He uses it in a number

01:02:09 of places to keep his documentation up to date. I've used Cog to an extreme extent in my GitHub profile

01:02:16 to, for instance, grab information from PyPI where I mentioned what my projects are and things like

01:02:22 that. Yeah. Yeah. Cog is one of those things that started small and it's just has chugged along for a

01:02:27 long time. And I continue to find more uses for it. Yeah. That's great. Colin says using Cog to document

01:02:33 CLI tools is Chef's Kiss. Yeah. So very nice. Very nice. We're getting to the end here. We're almost out of time, but luckily we're also almost out of things to talk about. Well, we're not out of them. We're stopping.

01:02:45 There's a lot. There's a lot. This is a small sampling. But here's one by Haidang that's awesome tools for the readme profile. So this is a lot of, let's do the test. Click on their profile and see how it looks. You know what I mean?

01:02:58 Yep.

01:02:59 Got to get a little more in there. So this is more of a collection, but we have readme's for projects, but also readme's for humans, right? You know, if you go to my account, you see a particular thing. Some people have really fancied that up with lots of things. And this project here talks about, well, what kind of cool stuff can you put on there that people might see?

01:03:20 I haven't looked at yours recently. What's your profile look like?

01:03:22 So it's not as visual as this. It has a few badges, but I used Cog to, for instance, pull in the six most recent blog posts onto my page. I wanted to do recent tweets, but that was going to be hard because Twitter API wanted me to authenticate. And half the time I turn away when I'm asked to authenticate against the thing, because that's the hardest part of the whole thing. And it takes away all the fun.

01:03:46 The main thing I used Cog for, I used Cog on my readme. And one of the things I did with it was to write Python code to generate that markdown syntax for badges and to put together shields.io badge URLs. So both of those things are complicated, right? Shields.io is amazingly powerful, but how you actually put all the bits of information into the URL is hard to get right. And it's fiddly. There's like ampersands and you have to quote them in the markdown or something.

01:04:13 It's a regular expression, yeah.

01:04:14 Yeah, I mean, it's just too intense. So I wrote Python functions to put together shields.io URLs. And then I called those Python functions from the Cog code in my readme.md. And there's a GitHub action that runs the Cog on it.

01:04:29 Whenever I publish a blog post, my blog publishing triggers the GitHub action that recalcs my GitHub readme. So the latest blog post is on the top of the GitHub readme. Like I said, you can take this a long way. I may have gone too far with this.

01:04:45 Oh, I love it.

01:04:45 But yeah, it's cool to see how the tools can come together and you can automate all of these processes. Again, to go back to one source of truth, my blog is the one source of truth about what are my blog posts. But the information is also on my GitHub readme because I thought that would be a useful thing for people to see when they look for me on GitHub.

01:05:04 Yeah, that's fantastic. All right. So this project here is like a whole host of things like that that you could do. And I love the use of Cog and the GitHub actions just to chain it together.

01:05:16 Awesome tool for readme profile. It's sort of like a blank catalog. Like you might want to put this on your profile or put that on your profile.

01:05:24 If it was 1994 and you wanted a blink tag, here's a whole bunch of or a little animated diggy GIF you could figure out.

01:05:31 So you get these graphs of like what were your last year contributions over time or when are you most likely to?

01:05:39 Yep.

01:05:39 Some more badges. Like here's the latest blog posts, which is a thing that people can pull in if they don't want to do more of it themselves.

01:05:46 Yep.

01:05:47 How much time you spent coding in various languages per month or per week, weekly here. That's pretty wild.

01:05:54 Yeah. He's got a lot of things here, like what you're listening to on Spotify.

01:05:58 Yeah. Do they have emails, one of your coding activities? Cause I spend a lot of time in email and I wish.

01:06:02 Are you typing code in your email? You might be doing it wrong.

01:06:06 I'm just spending a lot of time in email. I wish I didn't.

01:06:10 Okay. So it's got a, what time of the day? Are you a morning person? Are you a,

01:06:15 it has a snake game that goes around and races like a centipede.

01:06:20 You know, you're right. This is very reminiscent of the early, like geo cities kind of internet where

01:06:26 everything flashed and blinked and looked cool and had contrasting colors and stuff like that.

01:06:32 Yeah. So people, I mean, we're only like a third of the way through this game. People can,

01:06:36 they can give themselves trophies. They can give themselves, I think this is stack overflow. Yeah.

01:06:41 Stack overflow reputation.

01:06:43 There's just a ton of different stuff you can put together. And I think it all comes back to,

01:06:47 you know, besides like maybe overdoing with digging animated GIFs and blink tags. I think it comes back

01:06:53 to your GitHub profile is a little bit like your resume and how much can you say more than just,

01:06:59 Oh, I forked Django.

01:07:00 Right. And you want, I mean, the point of the profile is to let people know about you and

01:07:05 hopefully they'll be interested in you in whatever way you want them to be interested. So all of these

01:07:11 things that attract attention and let you can choose something here that sort of has your vibe

01:07:17 in whatever way. For instance, my page is very text heavy, but that's my vibe. That's the way I am.

01:07:22 And if that's not for you, then you should look for someone else's profile. But if you want to know

01:07:26 what I'm listening to on Spotify, then that's a thing to put on a profile page. So it's great. I

01:07:32 mean, self-expression is a wonderful thing. And the fact that GitHub lets you build your own profile

01:07:37 and that there are all these tools to do whatever you want with it. It's amazing.

01:07:41 It is amazing. All right. I think this is probably going to be it for our final thing to cover and

01:07:46 read me and friends. Let's close this out just really quickly with a, give us the, the 7.0 story on

01:07:53 coverage. Oh, coverage on 5.7.0. Yeah. That's a big deal. All right. I mean, if you're going to

01:07:58 make that big of a number, it might not be a big deal. This is a tricky thing. So really what happened

01:08:02 was I was looking through the bugs that people were reporting and a lot of them had to do with,

01:08:06 it couldn't find my source file where I said it should put the source file. And I was answering with,

01:08:11 well, you have to do these tricky things in your configuration file. And I thought maybe that should

01:08:15 be simpler. So really the reason it's a 7.0 is because I made things better, but I also think you

01:08:22 might have to change your settings in order for them to still work the way they used to work.

01:08:26 So when you look at the change log for coverage.py 7.0, there's no like amazing big thing. The biggest

01:08:33 feature change is that when you get a text report out, now it can be in markdown format instead of

01:08:38 in plain text format. And that's cool, but that's not like a 7.0 level feature. The real change is,

01:08:44 I think it's going to be better, but a few of you might have to update your settings. And I wanted to

01:08:49 make it clear to people that that was going to happen. So I bumped the number to 7.0.

01:08:54 That seems totally reasonable and still going strong. It's a beta one right now. When do you foresee

01:09:00 this becoming the pip install coverage sort of version?

01:09:04 That's a great question. I have to admit, to be perfectly honest with you, that I have been

01:09:09 disappointed in the past at how few people try out betas. So I'm putting this out there in a

01:09:15 disciplined way and I'm trying to talk about it, like go and try the beta, but eventually I'm going

01:09:20 to get tired of waiting for people and I'm just going to publish it. And if the bug reports come

01:09:23 in then, then we'll deal with them then because there's only so much you can do to get people's

01:09:28 attention on a beta.

01:09:28 Absolutely. I can totally understand that. All right. Final two questions before you get out of here.

01:09:32 If you're going to write some Python code, what editor are you using these days?

01:09:36 Vim.

01:09:37 Vim. Right on.

01:09:37 And I do not have any code completion plugins.

01:09:40 Okay.

01:09:40 I've said this before. I'm very low tech.

01:09:42 Perfect. And then notable PyPI package. I kind of feel like we've covered a bunch,

01:09:46 but if there anything you want to give a shout out.

01:09:48 We did cover a bunch. You know, I've been very enamored of Rich, I have to say. It's very cool.

01:09:53 I'm looking forward to hearing more about what Textual is going to be for building

01:09:57 terminal UI interfaces for applications. But Rich is astoundingly competent at what it tries to do.

01:10:05 Yeah. And what they're doing on the terminal is just nuts.

01:10:08 It is.

01:10:09 Nuts in a good way.

01:10:10 I only discovered just the other day, maybe people don't know this, that you can,

01:10:14 one of the Rich styles, and this is a feature that terminals support and Rich is just tapping

01:10:18 into it, but it gave a convenient way to do it. You can output text, you know, that's red or that's

01:10:21 bold. You can output text that's a link where the word in the terminal is just, you know, click here

01:10:27 and behind it is the URL you told to have it. And then you can click the link in the terminal

01:10:32 and go and visit things. Astounding.

01:10:34 I'm familiar with terminals detecting links, but not having a different link text than the actual link,

01:10:41 right?

01:10:42 Yes. That's what I'm talking about. I didn't know it could do that.

01:10:45 Yeah. That's nuts.

01:10:46 Yeah. Cool. Well, that's definitely a good one. All right. Final call to action. People are thinking

01:10:50 about their projects. I want to get started with some of these ideas. What do you tell them?

01:10:53 Think about your users. Think about who you're writing for. And it's different people at different

01:10:58 times and write, write words. I actually want to say one more thing. We talk about change logs as being

01:11:04 really good for the users of your library. I find when I sit down to edit my change logs that I

01:11:09 understand my own product better and that I think about the features I've built in a new way and

01:11:15 sometimes actually go back and change them because in the process of trying to describe what happened,

01:11:19 I learned something. Yeah.

01:11:21 Writing for readers is great. Writing, you will learn things when you write. Write more. It'll be good.

01:11:26 I can definitely see that. You're like, I want to say, but it doesn't quite do this unless I change

01:11:31 this other thing in code and then it'll be true to what I tried, wanted to say here. So yeah. Yeah.

01:11:36 Perfect. Yes. All right, Ned. Thanks for coming back on the show. Great to have you here.

01:11:39 It's always fun. Yeah. See ya.

01:11:41 This has been another episode of Talk Python to Me. Thank you to our sponsors. Be sure to check

01:11:48 out what they're offering. It really helps support the show. Listen to the Local Maximum podcast.

01:11:53 Learn about topics as diverse as the philosophy of probability and Elon Musk's next move.

01:11:59 Just search for Local Maximum in your favorite podcast player.

01:12:02 Take some stress out of your life. Get notified immediately about errors and performance issues

01:12:08 in your web or mobile applications with Sentry. Just visit talkpython.fm/sentry and get started

01:12:15 for free. And be sure to use the promo code talkpython, all one word. Want to level up your Python?

01:12:21 We have one of the largest catalogs of Python video courses over at Talk Python.

01:12:26 Our content ranges from true beginners to deeply advanced topics like memory and async. And best

01:12:31 of all, there's not a subscription in sight. Check it out for yourself at training.talkpython.fm.

01:12:36 Be sure to subscribe to the show. Open your favorite podcast app and search for Python. We should be

01:12:41 right at the top. You can also find the iTunes feed at /itunes, the Google Play feed at /play,

01:12:47 and the direct RSS feed at /rss on talkpython.fm. We're live streaming most of our recordings these

01:12:54 days. If you want to be part of the show and have your comments featured on the air, be sure to subscribe

01:12:59 to our YouTube channel at talkpython.fm/youtube. This is your host, Michael Kennedy. Thanks

01:13:05 so much for listening. I really appreciate it. Now get out there and write some Python code.

01:13:09 izepotletcwnc.com

