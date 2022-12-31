00:00:00 If you maintain projects on places like GitHub, you know that having a classy README is important and that maintaining a change log can be helpful for you and consumers of your project. It can also be a pain. That's why I'm excited to welcome Ned Batchelder, to the show. He has a lot of tools to help here, as well as some opinions we're looking forward to hearing. We cover his tools and a bunch of others he and I found along the way.

00:00:24 This is Talk Python to Me episode 395 Recorded monday, December 5, 2022. Welcome to Talk Python to Me a weekly podcast on Python. This is your host, Michael Kennedy. Follow me on Mastodon, where I am @mkennedy, and follow the podcast using at Talk Python, both on Bostodon.org. Be careful with impersonating accounts on other instances. There are many. Keep up with the show and listen to over seven years of past episodes at Talkpython FM. We've started streaming most of our episodes live on YouTube. Subscribe to our YouTube channel over at Talkpython.FM/YouTube to get notified about upcoming shows and be part of that episode.

00:01:17 This episode is brought to you by The Local Maximum Podcast Over@localmaxradio.com, and it's brought to you by Sentry. Don't let those errors go unnoticed. Use sentry. Get started at Talkpathon.Fm/sentry.

00:01:31 Transcripts for this episode are sponsored by AssemblyAI, the API platform for state of the art AI models that automatically transcribe and understand audio data at a large scale. To learn more, visit talkpython.FM/AssemblyAI.

00:01:47 Ned. Welcome back to talk python me.

00:01:50 Hey, thanks for having me. This is always fun.

00:01:52 Yeah, it's always a good time to have you on the show. Got such interesting things to talk about. I think we've previously spoken about coverage, stop, high beginners and experts and several other things. Probably if I go back through the.

00:02:06 Old search engine, I've had many opinions about many things.

00:02:09 Perfect. Well, we're looking forward to hearing your opinions on the title might suggest on the README, but I think maybe we got to expand it to a couple of other markdown files, maybe on a project as well to get the holistic picture. But basically we're going to talk about tools and ideas and techniques for making your project more accessible, more feeling, more polished and welcoming to people when they land on your project on GitHub or GitLab or wherever. So that'll be fun.

00:02:39 Yeah, it's an interesting topic too, because as a project maintainer, there's all this project level automation that goes on and there are all these fascinating tools to get parts of it done in different ways and competing philosophies.

00:02:50 Yeah, absolutely. I know some of them because I fork different projects and then I'll sync it or something and it'll say that my automation couldn't run. I'm like, well, that wasn't my automation, but that's okay, it's fine if it runs or it doesn't run. I'm just here to follow. But before we get into all that, maybe let's just do a quick recap for those of you, those listeners out there who don't know you, maybe what's the elevator pitch and what have you been up to the last six months or so?

00:03:14 I've been working in the python world for a very long time, I don't know, 20 years now or something crazy like that. But my day job is at Edx, which is part of two you now learning tech education, tech company, and I do open source logistics there. Edx.org runs open source software that we've created called Open Edx, which also runs a couple of thousand other sites. And my main day job is making sure that that collaboration continues well between the people inside to you and the people out in the community. So it's an interesting dynamic of open source. But on the side, I also maintain a number of projects, including coverage.Py, which has been going for 18 years now and is used by a lot of people. So that's a whole other kind of open source that I do in the python world.

00:04:01 Yeah, that's a really rewarding job. Right. It's not optimizing ad clicks or other things like that. Right. It's helping people.

00:04:08 Right. It's a noble goal. We're educating the world and we're giving away software to help other people educate the world. Yeah, it's really good.

00:04:15 Fantastic. And speaking of open source projects, I think we might touch on a couple more of yours as we get going.

00:04:23 Indeed.

00:04:23 Yeah.

00:04:24 They tend to multiply somehow. I haven't learned my lesson yet.

00:04:28 Yeah. Just got these puppies running everywhere. I don't know what's going on exactly.

00:04:31 They breed. I don't know when it happens.

00:04:33 They breed, exactly. All right, well, let's start off with one. I don't know if you're familiar with this README So. I don't know what the So stands for, but I think of this as README as a service.

00:04:44 Interesting. Yeah. Or stack overflow. No. So isn't Stack overflow? I don't know why they chose.

00:04:50 I don't either. The woman who maintains it works at GitHub. I'm pretty sure I won't go and find out when I get to the bottom, but I don't think it has an association with Stack Overflow.

00:04:58 Right. And usually two letters are country codes. I don't know what So stands for.

00:05:03 I don't either.

00:05:04 Country.

00:05:04 Sorry. So folks, but this place README So, it says this is the easiest way to create a README. Now, before we get into the details of this, maybe we should just talk about let me pull up coverage. Coverage.py on GitHub. Not to put you on the spot or that, I don't mean to do that, but let's just talk about that's.

00:05:24 Fine.

00:05:25 What kind of stuff should you put on your project? And like I said, we're going to have to expand a little bit. Like, for example, there's tags and there's a link and there's should you have releases shown and other stuff that you might kind of think of it what you get when you land on a project. So maybe start there with kind of how you think about what should be here. Then we'll talk about some of the tools.

00:05:45 The first thing your README should do is say what the project is, and that's sometimes difficult for people to wrap their head around. And it really gets at one of the fundamental problems of writing almost anything, which is you have to decide who you're writing for, and it's hard to know who might show up on your front page of your GitHub project. And you don't know what they already know, and so you don't know what you have to tell them. So it's a little bit tricky to get all that information out there. But, for instance, under about here, it says the code coverage tool for Python, which was the sort of pithiest, shortest description I could come up with to say, what is coverage.py? And I think that covers it pretty well. I don't try to explain what code coverage is, because that's a topic you can Google for if you don't know what it is, but so that covers it.

00:06:28 If you don't know what it is and you don't know you want it, you might not care about this. So that's not your audience.

00:06:33 Right. Why are you here if you don't? Exactly.

00:06:36 But go ahead and start on your way out the door, please. Thank you very much.

00:06:39 Right, exactly. Yeah. By the way, I could use a bunch more stars on coverage.py because it's not a JavaScript project and it didn't start on GitHub, so it's a little low on stars.

00:06:49 Yeah.

00:06:49 But so, yeah, so I try to say what it is and then how to get started on it. And I think those might be the front top two things. I've got a thing there about Ukraine and badges, which we're going to get to, but there's the first paragraph there. Coverage py measures code coverage, typically during text execution, so it tries to give sort of a little bit deeper explanation of it, what you can run it on and then getting started. There's a for enterprise thing there that links off to Tidelift, but then the getting started tries to be very quick about you just want to try it. Here are some commands you can run to see how it works for you, because a lot of people, they just want to get going and if you can give them a quick instruction, then they'll be really happy.

00:07:30 Yeah. Often four or five lines of code. Here's how you use my thing. Do I put a decorator onto a function and it does caching? Do I await a database call or what am I doing with this thing? Right? You don't have to be super complicated, right.

00:07:44 And sometimes it's not even clear. Some people forget to mention, is this thing an application? Or is it a library? Like just the big picture? Like as a developer, you can be so in the trenches with your code, you forget people don't know what it is yet, like what shape it takes. Now, my README is pretty short, and actually the getting started doesn't show the commands. It links to the getting started, the quick start section of the docs, and the change history links to a separate part of the docs. So it's actually a pretty short README. Some readmes can be very long, a little overwhelming. You have to scroll past all the getting started to get to the change history.

00:08:20 For instance, I decided to take a different approach, which was to make it almost like a table of contents to the places you might want to start in the larger docs.

00:08:29 That is a decision you have to make. Right. Do you try to put enough in there that it's it's basically standalone, in a sense, or do you do you encourage folks to find their way over to a much more holistic sort of place? Right.

00:08:42 That's an information architecture problem.

00:08:45 The thing about writing a good README is it's documentation. And documentation has challenges all of its own that most developers haven't been trained in formally. It's not really their first interest. It involves thinking about other people, which let's just say some developers aren't skilled at.

00:09:03 Also the curse of knowledge. Right. Once you know what code coverage is, you don't feel the need to explain it or set the state. You're just like, well, we want code coverage. Of course you do. And here's the tool.

00:09:14 Yeah. So it's hard to decide what words to put in there, how much to say, how to organize it. Those are all real challenges.

00:09:19 Well, it's quite popular with 7.5 million downloads a week.

00:09:23 Is that what it's up to? Yeah. That's crazy.

00:09:25 That's what it says.

00:09:26 That's kind of insane. Right. And it supports all the versions of Python, even the fast one. So that's cool.

00:09:32 Well, it's interesting. So this is the point we might get to later. So you're looking at the Python versions it supports on the badge.

00:09:39 Yes.

00:09:39 But if you actually read the text it's actually mentioned, which goes up the badge goes up to three point eleven. The text says it goes up to 3.12, the alpha alpha too. And that's because of how the badges work. And there's reasons why people don't like badges because of that. But badges look cool, so you want the badges in. What's going on here is that the badges show the status of the latest release on Pypi and so they're not in sync with what's in the repo. And it's kind of a challenge to figure out what you want to do about that. Unfortunately.

00:10:11 I do see, though, that you are a believer of badges.

00:10:14 I kind of got into badges there's. What do we got on screen here? Six rows of badges, which honestly is a bit much. And I should probably I mean, it's just kind of a mosaic of green and blue at this point, and it's kind of hard to get rid of.

00:10:26 But I'm kind of excited to see that you have a Mastodon badge, the newest one.

00:10:30 I put a Mastodon badge on there. Exactly. Because that's the new crisis is getting moving from Twitter to Mastodon.

00:10:36 I'm finding Mastodon to be a really nice place. I mean, sort of it is sidebar for a second. How are you thinking about this whole Twitter Mastodon open source community on social media thing?

00:10:45 Yeah, I'm looking at it as an opportunity to try out Mastodon. And the thing that's really struck me about Mastodon is how many names of bloggers from 20 years ago I'm seeing again on Mastodon that I had lost track of and thinking like, oh yeah, I used to read that guy's blog 20 years ago, and now we're connected on Mastodon. And so we're kind of resetting back to a more distributed personal style of communication. Twitter was great in that everyone was in one place, so it was kind of easier to find people. But Mastodon feels a little bit more like old Internet.

00:11:20 Yeah, it feels like open source social media. Not just the fact that the underlying code is but the philosophy of the federation and the different servers and the different smaller groups.

00:11:32 Right. There's some downsides to it, too.

00:11:34 The server I'm on had some downtime while they were, like, rejiggering all their infrastructure because they suddenly had 30,000 users and all right, I can do without Twitter Mastodon for 6 hours while they figure that out. And then they're back and we're going.

00:11:50 Yeah, I'm going to go for a walk or get some work done. Yeah, exactly.

00:11:54 Awesome. All right, well, that's a cool badge. We'll come back to badges later. I think that sets the stage. One more thing before we get into some of the tools. There's places like, I think Tailwind CSS might land in this realm.

00:12:11 It's just too popular to search. Let's see. Just the tailwind. CSS, please. Or I know Poetry can't search for that alone, but Poetry with Python, if you go to their websites, they've got like a fancy website.

00:12:25 Yes.

00:12:26 You know what I mean?

00:12:27 Yes.

00:12:27 And I see some open source projects like VJs maybe is like this, where it's almost like there's a marketing landing page for the project. And of course it is. They'll have like a dark mode button.

00:12:40 How do you think about this when you see this? You're like, oh, I need to do this. Or is this kind of I've never.

00:12:45 Been tempted to build a page like this, partly because I don't think I have the skills to build a page like this. And the things that I make are aimed at developers. I mean, you're showing a Poetry page landing page here, which is also aimed at developers. But I guess my feeling is developers don't need that kind of flash. And honestly, if people use a different thing because it's flashier, that's okay. I'm not out to corner the market.

00:13:11 Yeah, it's not JavaScript code coverage. It's not JavaScript.

00:13:14 That's right. But also, I think sometimes it can be a little misleading just to go back to Mastodon for a second. So one of the problems that people have with Mastodon is that they have to choose a server, and that's the first choice they have to make. And it's a difficult choice because it's an unfamiliar choice. If you go to join Mastodon.org, it's a flashy site with cartoon elephants and things on it, and it looks very easy. But then the first button you have to pick presents you with a choice that's hard.

00:13:41 Here's your thousand choices. Pick fun. Don't get it wrong.

00:13:44 It might have been less cognitive dissonance if the page looked a little bit harder, so that when you got that choice, you knew what you were getting into, it would kind of ease you into that hard choice. I can see actually, I hadn't looked at the page in the last few weeks. They've actually changed it from choose a Server to Create Account. Which is good, because that feels more like what you're doing is creating an account rather than choosing the server.

00:14:04 But you're on the page, it says.

00:14:06 Servers, which they'll smooth that out. They'll smooth that.

00:14:11 People used to be confused by Twitter. We figured it out. Yeah, I know, but I agree that it's an interesting kind of marketing angle for software, which is a little bit weird, right?

00:14:23 But I should say so coverage.py does have a mascot, which was drawn by my son. So it's got that cute aspect to it, but not the whole page isn't cute. And actually you're scrolling it on the screen. I'm noticing the mascot isn't on the GitHub.

00:14:38 Should I go to the docs page?

00:14:39 Yeah, if you go to the docs.

00:14:40 You'll see there we go.

00:14:41 There in the upper right.

00:14:43 Very cute.

00:14:44 Sleepy snake. Yeah. So I've got a little bit of that, but that's because I've got a son who can draw like that, and he made me a mascot. If he hadn't done that, I wouldn't have anything cute on the covered with a blanket.

00:14:54 I got it. Yeah.

00:14:56 He's relaxing because he knows his tests are all covering his product and he is sleeping well.

00:15:05 This portion of Talk Python to Me, it's brought to you by the Local Maximum podcast. It's an interesting and technical podcast that dives into trends in technology, stats and more. But rather than tell you about it, let's hear from Max and Aaron about their show.

00:15:19 We are now on with Talk Python to me. Let's say hi to all the Python fans.

00:15:23 Hi, Python fans.

00:15:24 I'm Max Clark. I have actually done a lot with Python myself, so I am a fan of Talk Python to Me. Do you know Python Aaron?

00:15:32 I took a course years ago, but I am a little rusty.

00:15:35 We are here today to talk about our podcast, The Local Maximum. We've been on a roll lately with a new episode every week and I wanted to share with you what we've been up to. Here on The Local Maximum, we tackle subjects in software and technology topics as diverse as the philosophy of probability to Elon Musk's next move for Talk Python listeners, I want to highlight a couple of recent episodes of The Local Maximum. In 248, for example, I found out about an open source library that maps the world into Hexagons and some Pentagons. I had a discussion with an author about games and puzzles and another on a novel approach to doing the job search.

00:16:11 Well, we discussed the ramifications of Ai generated art. Have we reached peak creativity? Or is this just another local maximum?

00:16:19 So check out The Local Maximum podcast available on your podcast app.

00:16:24 Okay, well, I think that sets the stage for this conversation pretty well. Let's talk about README as a service. Have you played with this any so.

00:16:31 I haven't played with this. I tend to be very low tech in the way I approach things. Edit some text files, build some tooling to make the result you want and get going. So this looks like a good way to get started. Like if you don't know what to do, this looks like a good on ramp. So it looks great. If that's the way you like to approach things, definitely do it. My philosophy is any way you can get a good README is a good way to get a good read me. So if this is going to help people, then I'm all for it.

00:17:02 It's not something you tie into your README. It's a web app. And it looks like one of these marketing page landing page builders on the left. It's got a bunch of different sections. Like you can drag them in, so you drag in the title and description, you drag in the acknowledgments and fill it out and it will create the skeleton markdown and then you just take the markdown and run with it.

00:17:22 Right.

00:17:23 But it gives you a lot of structure, like, well, here's how a lot of people put their author acknowledgments or here's how they put their example code or FAQ.

00:17:30 If this is so, I haven't played with it, but if the output of this is a markdown file that you then own and edit later on, this is just a sort of a quick start templating thing.

00:17:39 I'm pretty sure that's how it works. Yeah.

00:17:41 Any way to do it? I'm personally always a little bit skeptical about new tools that I have to keep in my tool chain and keep working and the hope will remain maintained. Personally, like low tech approaches, like I said, I have a text file that I can edit. Great, I'm all set. So I like that this tool is a way to get started, but then gives you the text file that you then own.

00:18:04 Yeah, exactly. So when you're in a section, you just are working on these various pieces. It kind of is like a function.

00:18:13 I'm just editing the internal, but it puts it all together in the whole thing and you get just a raw mark down with a copy button. And it seems pretty neat to me.

00:18:21 It is neat because some of this stuff can be overwhelming. I mean, markdown syntax is designed to be as straightforward as possible, but once you get to badges, which are images with alt, text with links, the syntax is no longer simple and it's hard to remember how to do it. So having a way to mash a button and have a badge show up on the page. Great, let's do it.

00:18:41 So this was created by Katheriner and yeah, she works at GitHub. So that's pretty cool. But yeah, it's just basically a start from scratch and generate if you don't have a good example. So I kind of like that one.

00:18:54 Yeah. And GitHub in general has one of their philosophies is will make on ramps for people to do open source. Right. And then like, they've got in their documentation and their help, they've got how to use a console, which isn't their problem to solve, but they know that people are stuck getting into GitHub if they don't know how to use the console. So they're teaching people how to use the console. They've got choosealicense.com because people don't know how to choose a license and they need to in order to do open source well, and so on and so forth. So I love the on ramps that GitHub has built for these things.

00:19:25 Yeah. And just the community as well. Right. If you put your time and energy into this, there's a chance that people will come along, appreciate what you've built and contribute to it, as opposed to.

00:19:35 It'S a social coding site. That's their tagline.

00:19:37 Yeah, that definitely is. They seem to be living up to it. Okay. Another one that comes from this is.

00:19:42 The other end of the spectrum.

00:19:46 There's a couple of other ones here. This is from Hennock. This is your fancy project deserves a fancy pants read me based on hatch or with hatch, right? Yeah. So what do you know about this one? Have you done anything with it?

00:19:59 I looked at this a bit and this looks, like I said, the other end of the spectrum. So README So is kind of a visual, graphical way to get started. This thing, by Hynexlowak is a templating tool where you can automate the putting together of your read me from different bits of information from all over your repo. And it is a little bit overwhelming. How much is there? You look at the examples and you're editing Tomo files with five dotted nested sections to get the right pieces in place.

00:20:32 There you go.

00:20:33 And I totally understand this because I have built tools like this too, where I thought, you're a developer, you can write me a regex when it comes time to tell me what to do. So I totally understand this and I need to look more at it because it looks like it solved some problems that I might be facing myself and my own. Like, if you look at the coverage Pyrepro, there's a lot of custom tooling to do these sorts of things. And if I can find other people's supported tools to do the right things, I would like to use them. I mean, like I said, I tend to spawn new side projects when I need tooling, but that's not a scalable solution to things. I should use other people's tools more.

00:21:10 If they built some good ones that are out there. So let me see if I can find a section. There's a little part that's it the impressive thing.

00:21:17 So when I first came to this, I thought, I haven't heard of this hatch fancy PyPI README project, but under showcases. The Black README is built using this tool. And that's fine credential right there that the Black project is using it.

00:21:32 Yeah, absolutely. And you've also, as well as a bunch of others yeah, structlog and JSON. Schema.

00:21:38 JSON schema, yeah.

00:21:39 So maybe I could read this one paragraph and this might give people the sense. Do you want your PyPI README to be the project README, but without badges, followed by the license file and the change log section only for the latest release? Well, you've come to the right place.

00:21:53 So it's like he's got this whole assembly line model of there's already a bunch of information out there, so don't copy it around, don't try to write it in two places. Instead, have a tool pick up the information and then put it together into the README, which is what you want. And I totally understand that because I've done some of that kind of tooling myself in my projects so that I can put a piece of information in just one place and then it goes to where it has to go to be read.

00:22:19 It's a bit like a static site generator. A bit, a little bit.

00:22:23 The thing I still haven't wrapped my head around here. Is that what feels like? It could be one template MD file or something that says, you know, grab this from there, and that from there is instead in your Pyproject.toml sections so you don't end up with sort of what looks like a README MD file with call outs to where the information should come from. It's pieced together from the Pyproject.Toml sections.

00:22:48 I see. The toml will let you reach into the different segments of the thing in this area.

00:22:53 Yeah, and I understand why he's taking that approach because the Pyproject toml is there, and this is a hatch plug in, so he's already got access to that information and it's bolted into the process of building the distribution, which is the exact best time to build the README.

00:23:10 So it's cool that he's explored it this way. I have to take a deeper look at it to see if it would fit in with my workflow. I don't use hatch.

00:23:17 Yeah, hatch is nice and hatchling is nice and I've done a little bit of a little bit of work with it, and I can see why, if you're already working in that mode, how to kind of extend it.

00:23:27 Absolutely.

00:23:28 One of the problems with coverage.py, which is my main side project, is because it's 18 years old, there are bits of it that are using the latest, greatest technology as of 15 years ago. And because it's just kept working until it breaks, I'm not going to go and fiddle with it or until I'm interested in fiddling with it. I might fiddle with it, but there's a lot of stuff that's just old and weird and just keeps rattling along.

00:23:51 For such a highly used project, I can see the danger here, but have you considered, or have you run it through things like Flint to convert all the strings to F strings? Or some of these, like, upgrades to the latest Idioms, where you can say, I want it to be 37 and above, and anything that's older than that, you know, kind of rework it.

00:24:08 I have used Py upgrade on it when I dropped 2.7, which was a couple of years back, and there are now F strings all through it. But for instance, I don't use black. There is a pull request to add type annotations to it, but it's a big project that not gaining the momentum it needs to get done. So I tend to let sleeping dogs lie where it's working, or if I don't, I don't know what I'm going to get out of it. For instance, I use Opt Parse to parse the command line arguments, and that wasn't even the right thing to use in 2.7. That was the old thing that Arg Parse replaced. But it still works. It's still in there. Parse, it's fine.

00:24:48 Sometimes there's no value and possibly adding bugs to something that you don't intend to touch at all.

00:24:54 Right, right, exactly.

00:24:55 But maybe if you were to say, we're going to really dramatically expand the way that it can take arguments and do things well, then maybe all of a sudden you aren't like, we could get more flexibility with a new thing, but if you're not going to touch it, then just let it be. All right, let's get to the next one here. Shields IO. Yes, if you want a badge, come to the place.

00:25:14 They will make a badge for you. And Shields IO is a very impressive service, I have to say, because they give you. Lots of ways to make badges, including ways that I didn't even understand they could do. I found this out, actually, when I made that Mastodon badge, that you can tell Shields IO to go and grab some JSON from some other website and extract data from that JSON response and include it in your badge.

00:25:39 So you just call the Mastodon API, public API, to get stuff about your account and pull it.

00:25:45 If you look at my Mastodon badge, which is on Github/nedbat or on the coverage PY page, it has my count of followers, and that's coming from a JSON response from the Mastodon API on my server, on my Mastadon server then Shields IO is incorporating that number into the image that it then serves to GitHub to display into the README. I don't want to think about how many computers are actually involved to get that stupid number on that page, but it's very impressive that it can do all that.

00:26:14 I sure hope it's cash somewhere.

00:26:17 I hope so.

00:26:18 I don't know how interesting.

00:26:19 Yeah. They've got a bunch of these pre built badges that can tell you all sorts of things, like what version of your project is current on PyPI and what Python versions it supports, and what your licenses and all sorts of things. It's very impressive.

00:26:33 Yeah. And it supports not just Python, but I saw NodeJS. Nougat PowerShell.

00:26:39 Yeah.

00:26:39 Stuff that I don't spend as much time on over here.

00:26:42 Yeah. There's things I've never even heard of that it shows. They don't even document all the things it can do. I mentioned earlier that the badge on the PyPI page will show the status of the latest PyPI release, which means if you go back ten years to the coverage.py version three release, there's a badge on it that shows you that it supports Python 311, because the badge is showing you the most recent release. Even though you're looking at the badge on the ten year old release, there's a syntax in Shields IO that will let you say, show me this factoids as of this particular release. 3.0 I see. And they don't document it, so I didn't realize I could do that. So there's an awful lot going on in Shields IO.

00:27:21 Yeah. So if you want a shield for one of those little badges, for basically anything, these are downloads, users, test coverage, all these things.

00:27:32 Basically, they give you a URL that you put in into your README, and that becomes the badge as it resolves. Right?

00:27:40 Right. The URL returns you an image with the information on it that you want. Either information that you put into the URL, you can just make a URL that says, Michael Kennedy is cool, and it will return to you an image that says, Michael Kennedy is cool. So it'll just format things for you, but it also has ways of getting information and then formatting it to give back to you.

00:28:00 Okay. You probably could put this personally onto places not just on your project, but maybe on your GitHub profile. Potentially.

00:28:08 Absolutely. Yeah. Mike the social. I'm embarrassed to talk about how overautomated my GitHub profile page is.

00:28:17 I love it. All right. Shields IO That's a section for the live badges. This one is hot off the presses. Let's see if we can find oh, it says initial commit. We got it ten days ago. Will McGougan of rich, famous, rich and textual. And textual. Yeah. Put out a tool to generate a GitHub flavored FAQ markdown document. This is pretty neat.

00:28:42 This is a tool. I just took a quick look at it. It's in a similar vein that you want to make little bits of information in a convenient way and then have it published as a monolithic piece of information.

00:28:54 In this case, he's talking about FAQ questions, and I think he said somewhere here. I got tired of answering the same questions over and over, so I made a tool to make an FAQ or something like that. Yeah. I don't have the same problem of needing FAQs produced or why it's easier to put them all in separate little files that are combined together later than just editing one big FAQ page. But Will is a smart guy. He must have had a problem, and he solved it with this tool. And it's cool to see this is.

00:29:20 A little more similar to the way you described how you might see building up the README. Instead of defining an toml file, reaching into a giant document, have a bunch of small ones that get assembled into a result here.

00:29:32 Right. And that's a lot like some of the change log management tools that we're going to get to also.

00:29:37 Yeah. One of the things that prompted Will to do this, he says here is people will ask the same question over and over, and he in issues, and he's like, I just can't answer it again. How to make a table, or can I make a table? Yes, you can make a table. Here's the link, whatever that is. So it has a fuzzy matching on suggest. So I think this is why it's separate, because you can put alias questions to the frequent question, and then you can just on the terminal, on the shell, you can say Factories suggest. And if you have some kind of input to it, like, I took the question that somebody asked me, and I want to point them at the thing so I can just jam that into the terminal and it'll go actually, that matches over to this FAQ response. I think that's the idea.

00:30:28 And he says that it's designed to be used with a GitHub action to post an automated response on an issue. I guess is the point is that if he's getting a ton of issues that all need to be answered, instead of saying, go and read the FAQ, he's automated the process of putting the answer right onto the issue, which is cool. I didn't realize that aspect of it, so that's very cool.

00:30:49 So this is all of ten days old. People can check that out if they want.

00:30:53 Hot off the presses, torn from today's headlines.

00:30:56 Exactly.

00:31:00 This portion of Talk Python to me is brought to you by Sentry. How would you like to remove a little stress from your life? Do you worry that users may be encountering errors, slowdowns or crashes with your app right now? Would you even know it until they sent you that support email? How much better would it be to have the error or performance details immediately sent to you, including the call stack and values of local variables and the active user recorded in the report? With Sentry, this is not only possible, it's simple. In fact, we use Sentry on all the Talk Python web properties. We've actually fixed a bug triggered by a user and had the upgrade ready to roll out as we got the support email. That was a great email to write back. Hey, we already saw your error and have already rolled out the fix. Imagine their surprise, surprise and delight your users. Create your Century account at Talkpython Fm/sentry and if you sign up with the code Talkpython all one word, it's good for two free months of Sentry's business plan, which will give you up to 20 times as many monthly events as well as other features. Create better software, delight your users, and support the podcast. Visit Talk Python Fm/sentry and use the coupon code talkpython We talked about contributions and how people appreciate getting credit for participating.

00:32:23 I'm sure there are people who have closed a small issue or found and fixed a small bug and coverage up high or added a small feature and feel really proud of that, right? But they would feel more proud if you acknowledged that they did it.

00:32:37 I accept your PR. Right, of course.

00:32:38 Right.

00:32:39 So tell us about this all contributors place here.

00:32:42 This is a GitHub bot that on an issue you can say at all. Contributors add Michael Kennedy to the bug fix sections of the contributors because he did it right here in this issue that we're talking about. And that's really cool because I don't use this tool. Like I said, I tend to be very low tech. I do acknowledge my contributors, I'll mention them in the change log, and I have a contributors. Txt file that lists everyone who's contributed in some way. And I will hand edit that. And it can be I have to remember to put it over there and put it over there. I don't get so many contributions to coverage.py that it's a burden. And I kind of actually like that little sort of moment of Zen of finishing the paperwork and crossing the t and dotting the I's. But if you're on a big project where you are getting a lot of contributions. I could see how doing this with a bot would be save you that little bit of work that could become a big amount of work and you don't want to skip it. Right. Because like we said, it seems like a small thing to us and maybe like I don't want to have to bother, but it's a huge thing to the contributor to have their name mentioned. Yes. Yeah.

00:33:47 And maybe not just pride. Maybe they get a job because of it. Right. They could say, I'm getting hired to work on Flask. Look here, I'm listed as a contributor on Flask. That puts me above 99% of the other people applying, at least in that regard.

00:34:00 The Internet is the kind of place where when you get a little connection like that, you never know what it's going to lead to.

00:34:06 Yes.

00:34:06 There's all sorts of things that pop up because of the strangest little mention.

00:34:11 So true.

00:34:11 You might get invited to be on a podcast just because someone mentioned one of your dopey little tools on NASDA Dot.

00:34:17 Or you might even start a podcast.

00:34:19 You might even start a podcast. Yeah. Watch out, danger ahead.

00:34:22 Then you're really in for it. So the way that this allcontributors.org bot seems to work, I don't use it personally because I don't have projects that are big enough to really justify this in terms of open source projects, but in the comment on an issue or on a PR or one of those types of things, you can just say at all. Contributors, please add at GitHub name of contributor. And then it says for design or for bug fixes or for documentation. And then the bot says added them as contributor. That's really cool.

00:34:54 Yeah. So, like I said, I have a text file. One of the one of the unusual things I do with my text file is that when I build for coverage Pi, when I build the release, if you go and look at who who the author of coverage.py is, it says Ned Batchelder and 137 other people. And that number 137 is counting the number of lines in the distributors text. Because I wanted to be clear that yeah, it's not just me. There's lots of people helping with this. And you can help too.

00:35:20 Yeah. Especially over 18 years.

00:35:22 Well, yeah.

00:35:23 All right. Getting to the part of expanding beyond just README MD, but the broader experience of things that maybe gets the way pulled back into the README is a change log. Are you familiar with keepachangelog.com? Have you seen this?

00:35:39 I am very familiar with Keepachangelog.com.

00:35:41 All right, tell people about this.

00:35:42 So Keep a Change Log is basically an advocacy site that says you should really have a change log. And here's what we mean by that and why should you do it? And I absolutely agree with the idea of keeping a change log, which is a running history of what has changed in your project and that's because people that your users want to know what's changed. I mean, it sounds really simple, really basic, but I think people can approach it in really simple ways that aren't as valuable. And if you put a little bit more work into it, you'll find it's really, really valuable.

00:36:15 And you need to know, as a consumer of a library, is there an immediacy to this new version that I need to pay attention to? Is there a risk to this new version that I should be aware of? Or do I don't care? And I just leave my thing pen the way it was before. Right? If it says there's a CVE where if we send the dollar sign it takes over your server, you should get in there straight away.

00:36:36 Yes, exactly.

00:36:38 But if it says we deprecated this thing that you were depending upon, like, well, don't just push it, we're going to need to think about this.

00:36:44 Right? And I think the way you just described that is really good, which is that the user of the tool, the library, the application, they want to understand what's in it for me, like, from my perspective, what has gone on with this library. And I think that's one of the things that's difficult for people for maintainers is to put themselves in their users shoes and think what's changed about this that matters. There are some autogenerated change logs that, for instance, just put all the get commit messages in the change log. And those drive me nuts because they're telling me all sorts of things that I don't care about. I don't care that you restyled changed all the spaces to tabs in some file. That doesn't matter to me, that's just noise.

00:37:25 You're burying the lead by telling me stuff that doesn't matter. So keep a change log is a good, like I said, advocacy site. They have their guiding principles. Change logs are for humans, not machines, things like that. And they advocate for marking your commits with or marking your change logs, putting them into sections of what's been added, what's been changed, what's been deprecated, so that people can zero in on what matters. Right? Deprecated means I can't use the thing anymore and I need to make a change. And security means I really better get on this or I might be in trouble. So it's good to highlight those things and put it into the user's perspective.

00:38:01 I like the guiding principles here about for humans. Every version should have have one. The release date should be specified. It's it's easy to just say, well, version 2.1 had these changes like, well, wait a minute, more than three. Like, was that last week or five years ago?

00:38:17 How relevant?

00:38:18 Date things. I mentioned my son doing art. I always told him when he was a kid, put the date on the picture so I'll know how old you were when you made the picture and you never wanted to do it. But change logs, you can put dates on things. Like you said, you don't know how long ago something was.

00:38:32 Yeah. Don't have to go back and dip the thing to figure out when it was committed.

00:38:35 Right. All right, then we've got one chat from a viewer talking about creating change logs as a good job for AI. And these days, I don't know, 2022, not only is Twitter versus Mastodon, but chat GP. What's it called?

00:38:49 The AI TP three, I think something like that amazing.

00:38:54 And I can probably retire soon because it's going to do my job, I think.

00:38:58 Just yell commands. Just yell stuff at the computer from the couch computer. Go write the website.

00:39:04 Just make it better.

00:39:05 Scale the website computer.

00:39:08 Exactly.

00:39:10 Yeah, that's a good point. Mario out there says it's called Skynet. There are some amazing tools, like a bit of a diversion, but there's like this thing called Jasper a friend just told me about. And what you do is it's like Google Copilot for writing content and there's a bunch of crazy things out there.

00:39:28 Yeah, we've seen a complete change in the progression of things and it's astounding it is.

00:39:35 All right, well, let's get to one of the first tools that got you recommended. The reason I invited you is because I asked people for general recommendations and they kept recommending your tools and like, all right, well, I should just have gone to the show to talk about this.

00:39:47 I'll just come and talk about all of it.

00:39:49 All right, so we saw the Keep a Change Log ideas, but that's in theory, not in practice. Right?

00:39:55 Right. The Keep a Change log just says, look, you should write this stuff and here's how you should write it. It's not a tool, it's just encouraging people to do a good job. I looked around at tools when I wanted to get people to make better change logs, and there was one called Town Crier from the Twisted Project, and they solved the problem that a lot of change logs have. So if you just have a change log file and everyone who makes a change to the code is supposed to put an entry into the change log file, then that file becomes a merged conflict every time. Right. Because I added a feature, I put my thing at the top. You added a feature, you put a thing at the top op and it's a merge conflict. Years ago at work, what I tried to do is have a change log file and I told developers, put your change near the top of the file in the hopes that they wouldn't merge conflict. And developers would come to me and say, what do you mean by near the top of the file? Because they're engineers, they need precise directions. Right. So, okay, that wasn't going to work. So the idea that town crier uses and also the c python source code has a thing called blurb that does the same idea, which is when you make a change to the code, you also write one small file. Which has just the entry for the change log in it. And you check that in. There's a special directory that just has those little fragments in it. And so when you make your code change, you also add a fragment to that directory. And then later, when it's time to actually make a release, all those fragments can be concatenated together to become the change log. And the good thing about that is that you don't have merge conflicts because everyone creates their own fragment. They have unique names based on some principle, and then at publication time, when the release is made, they can get concatenated together. And like I said, Town Cryer did this and Blurb also did this. I looked at them and they were both a bit more opinionated than I wanted. I knew that if I was going to get a lot of people to use this thing that it needed to be very, very flexible. And I actually took an approach when I was building SCRIV of what's the least opinionated I can be? How many different ways can I let you decide how you want it to work? At the time, Black was rising in its popularity and it was famously opinionated, and so I sort of took the opposite approach.

00:41:58 Nice scrivs.

00:41:59 The idea is that it's got a few commands. You say scriv create to make a fragment, scriv collect to collect them all together. Those are the two main ones.

00:42:07 SCRIV looks like it looks like a great tool. And it looks like one of these things you could pip x install. Because you're not going to, it's unlikely you'll depend upon it for your code to run. You just need that command around to manage a project, right?

00:42:21 Or you can put it into your development requirements. Text, however it is, you manage your project tooling. But sure, pipx would work too. And it's actually grown one other command for making GitHub releases. So it will actually parse your change log file. Even if your change log file wasn't made by SCRIV, it will parse your change log file and then create a GitHub release from your change log file, which gets at a philosophical opinionated point of mind, which is that the information should live in just one place. And that place should be a file that you check into git. It should be a file that people can clone when they clone your repo. If they want to just look at the change log in emacs or whatever locally, they should be able to do that. And since you don't want to duplicate information but people do seem to like having GitHub releases publish a GitHub release based on the information from the change log file, rather than having the release be the source of truth, where it can't be cloned, it can't be edited.

00:43:17 There's no commits that you can track to see who put that text there, those sorts of things.

00:43:22 Okay, that makes a lot of sense. Let's see, out of the audience we got in the question last change, all I read was for Python 311. Did you read that? Have you read it's? A bit of a novel to see.

00:43:32 Python developers have taken to heart the idea, and I make it sound like this is a recent development. They've always done this. You know, there's a Python 311 has a What's New in 311. And they tend to be very detailed about putting stuff in the What's New document. And like I said, they've got their own custom tool called Blurb, which is how C Python core developers, they write what are called news entries, which get created as small files in a dedicated directory, and then those get aggregated into the What's New doc.

00:44:02 In that change log, there's 180,000 words. A typical novel is like 80,000. So that's a proper change log right there.

00:44:10 There's more information there than any one person needs, but everything that's there, someone.

00:44:15 Does need that's, right. And each one of those links to like, a GitHub issue or a Pip or something like that.

00:44:22 And there's a lot of those. I just noticed, I think it was today that they got GitHub issued number 100,000 in the C Python read. Wow.

00:44:29 Okay, that's major. It's been chugging along for a while. All right, so this looks like a great idea. What do we got up next? I just also wanted to just give credit, speaking of GitHub credit, from Colin Sullivan, who sent this in, amongst some other things as well, over on Mastodon. So thanks for sharing that. This is another one. I'm going to go quick because it's not a Python tool and it's actually in a technology I've never heard of. Maybe you've heard of it, Ned.

00:44:52 So I hadn't heard of this. So this is called Change Log Manager from Masukoni, and it's interesting that he, masukoni is one of those bloggers from 15 or 20 years ago that I'd lost track of and suddenly got reconnected to on Mastodon. And when I asked about I, I got a little petulant on Mastodon about a change log that I found completely useless. And he chimed in with a long thread about how aggravated he is by change logs and how hard it is to get people to do them well, and pointed me at this tool that he had written about it.

00:45:22 It looks like a cool tool. People can check it out if it works. Well, it's written in a language called or technology called crystal.

00:45:30 Yeah, I don't know what that is.

00:45:31 Makes me feel old all of a sudden. Not even know that that was a language I don't know. But wait, hey, look, Colin's out in the audience. Hey, Colin.

00:45:41 Thanks for the recommendation you got me on here.

00:45:43 Yeah, absolutely. So this is a cool project here and people can check it out and yeah, it's got a lot of the philosophy of how you should do it, how you shouldn't just have commit messages. I remember hearing about tools that would look for swearing and other kinds of frustration in commit messages and not allow those particular messages to get into the change log. But I don't think that, as you pointed out already, that individual commits are generally the right granularity.

00:46:13 Right. Commits definitely are not. Some of these tools will aggregate your pull requests to be the change logs, and that's a little bit better because they're larger grained. But even so, I think there's real value in hand curating your change log. Start with a list of pull requests, but then take a look at it, reorder them so they make some sense and tell the story.

00:46:34 Right. Put the important stuff on top.

00:46:35 Put the important stuff on top. If you have three pull requests, which just by coincidence, all changed how you, you know, handle file matching, then make an entry that says, we changed a bunch of things about file matching and then have sub bullets about the file matching changes. You know, you want to explain things to people and you're going to be able to do a better job of it than your pull requests or your commit messages.

00:46:55 Absolutely. All right, well, thanks for that, Colin. Executable Books. Executable books. Folks are interesting. They've got a lot of tools that will take jupyter notebooks and other things using the miss plugin for markdown and generate books in different ways. And so they've got this project called GitHub Activity, which generates a simple markdown change log based on that. Let's see, I think this is on issues and PRS, not commits.

00:47:26 Yeah, I think this is one of the ones that goes for the larger, larger, chunk bits of information, which, like I said, is good. Commits are too small.

00:47:34 The issue is still that when you write a pull request, what you're writing about mostly is something that your reviewer needs to read. Right. So you're really addressing your your collaborators rather than your users. I mean, ideally, your pull request would include all of the user consequences as well, but it's also going to talk about what your collaborators need to know. So different audiences, different information.

00:47:57 At the very least, it's going to need an editing pass in order to figure out how to actually explain this to people the right way.

00:48:03 Sure. Well, that's an interesting idea. Maybe the the tools don't have to be perfect. Maybe they could say, well, here are the ten things in terms of PRS and issues that have changed. Now just rewrite that for humans, a different audience that still could be valuable.

00:48:17 Yeah. Collecting up all the information. That's great. I just think it needs a human touch.

00:48:21 Yes.

00:48:22 That's controversial in these days of AI, but I think humans can do a good job writing.

00:48:27 Indeed. As we say, Get a copilot, write me a network. So the next one we come to is Dinghy. Dingy, dingy. Okay. Dingy. Got it. Just like the little boat thing.

00:48:37 Yeah, the little boat. That's right.

00:48:38 Okay.

00:48:39 Yeah. So this is a tool that I wrote. And it was interesting because when Colin mentioned this as a tool for change logs, that's not why I wrote Dingy. Dinghy is designed to give you a daily digest of GitHub activity, which, by the way, is why it's called Dinghy, because the di stands for digest, and there's a GH in it, which stands for GitHub. And I looked through words that had those pairs in them, and Dinghy popped out nice.

00:49:00 It's got a Y, which is like half a python for pie, and it's got Leaos.

00:49:04 And then you can backfill the marketing slogan of your lifeboat on a sea of information or something like that.

00:49:10 There you go.

00:49:11 Dinghy gives you a digest of your GitHub activity. I was finding at work that I had to track lots of issues and pull requests, and there were lots of repos where I wanted to know what was going on. And so I found it useful to just summarize the activity on issues and pull requests across repos.

00:49:27 Nice.

00:49:28 Yeah. In the morning, take a look what happened on the last day. Oh, I should dive deeper into that one. I can click into it and go read the real issue, but you just can get a quick overview.

00:49:38 So I use it sort of on a daily basis. But I can see how you could take this and get a digest of the last three months and then use that as at least a guide to where to get the information for a change log, if not pulling information right off.

00:49:52 It seems real helpful if you work on a team, especially if you're the team lead or kind of a manager type, and you're like, all right, I just need to see what's happened on these three projects this week.

00:50:01 Exactly.

00:50:01 Just hit it.

00:50:02 That's what it's for. And it's satisfying to hear people think of other uses for it. That's the sign of having built a useful tool, is that I meant it for one thing, but then someone else sees, oh, I could use it for that, too. And that's very gratifying.

00:50:15 I can see at the end of a sprint, like a sort of post mortem burn down type of thing.

00:50:19 Yes.

00:50:20 Okay, cool. You mentioned blurb. I'll just put a link to the Blurb project tool as well. This is the C python. Prolific writer.

00:50:30 This idea of building the change log from small fragments is something that's happened a number of times, and I think it's a great idea. I think it's the right way to do this kind of work.

00:50:40 Agreed. One that comes. Is this GitHub itself that does this? No, there's not. There's a thing called release drafter and it drafts your next release notes as PRS are merged into a master. Okay, so I haven't used this.

00:50:55 This is another case of things going into GitHub actions and I'm fascinated by this whole thing. As a project maintainer, I feel like there's sort of three large buckets of work. There's the building, the product itself. I don't mean product to sell, but like coverage a product there's maintaining the test suite for it, which is if you've got a large test suite, is a whole endeavor all to itself. There's all this project automation that we've been talking about here today. How do I get the releases made? I've got to make file, what this command?

00:51:24 How do I bump the version up? All of that kind of and it feels like MicroAutomation. You're doing it like one shell command at a time or a ten little python, ten line python file or something. And the fact that there are all these tools around that help with it and put it in GitHub actions and you make a git tag and suddenly it goes to PyPI and publishes the GitHub release and all that. That's fascinating to me how far you can automate those processes.

00:51:48 They kind of build up like a snowball going downhill pretty quick. Because you're like, well, if I could automate this thing and that thing, they're like, wait a minute, now they click together and then we're almost there.

00:51:59 I'm a late adopter of technology. I won't automate a thing until I know that it's exactly the way I want it. And I've gotten completely sick of doing it by hand. Yeah, but the good news is, by then I do know exactly what I want it to do and so I can build the automation and I don't have to come back and fiddle with it too much.

00:52:14 Another big benefit I would say to that approach is every time it runs, it could just warm your heart with a joy. Like you know what? A whole another 2 hours I didn't do that thing.

00:52:23 That's right. The downside is when it does the wrong thing. So this weekend, I actually had a big weekend this weekend. I released 1.0 of both SCRIV and Dingy and the first beta of coverage 7.0. And it turns out that the links to Pipi on the read me, the links to my documentation from the PyPI README are broken because they don't work if it's a beta release. And I didn't know that until the release was published. And betas happen. So infrequently it'll change again before I make another one. And it'll probably be broken too, because it's hard to test this kind of automation. Like the good thing about building the product and building your test suite for the product is that that is automation. You can run the crank on and you know, if it's working or not releasing projects. If you build automation for that, how do you test that? If release happened correctly, other than actually making a release and then getting bug reports from people about the 404S on your PyPI page? Which is how I found out about this. Yeah, it's a little frustrating, but for.

00:53:21 As much fantastic testing software and automation, sometimes you got to hold your breath and push the button.

00:53:28 And you're not going to write a unit test that says, let's push this thing to test.pypi.org and see if all the links on the readmeer right. That's maybe you I guess you could, but you could. If anyone's done that, please get in touch because I messed that up this weekend.

00:53:43 Yeah, at some point you got to go, okay, we've tested enough, it's got to go. And even if you write a unit test, it's not necessarily exactly the same.

00:53:52 It's not the same and you'll fiddle with it and break it, which is what happened to me.

00:53:57 Yeah, absolutely.

00:53:59 There'll be another release. It's fine, there'll be another release. We'll get it fixed. All right.

00:54:03 You mentioned town crier already. I think maybe we can carry on, but people can check that out as well, I guess. Give them a quick shout out as well while we're here. This comes from the Twisted project, he said.

00:54:13 Yeah, and Twisted is another of these projects that's been going for a very long time. So this is a mature tool. It's just a little bit quirky in the way that they wanted to do things. I think at least when I first looked at it, it was something like the fixes went into a dot fix file and the features went into a dot feature file, things like that.

00:54:31 And it didn't do Markdown. And I knew that I was going to have people who needed Markdown, even though I prefer Restructured text. So I built Script to kind of along the same ideas, but in a more flexible way.

00:54:43 Right, okay, cool.

00:54:45 One of the things you may have in your README or other parts of your documentation, your markdown files or Restructured text, I suppose would be example code, like I talked about, that it would be nice to know some level of correctness to that, right?

00:55:02 Yes.

00:55:02 We have MK test, docs. Tell us about this.

00:55:05 This is one of these things. The interesting thing to me is that you've got docs, you've got tests, you've got doc strings, and there's all these tools that do all the different pairings of stuff, right. So you can run tests against the code in your doc strings. This runs Pi test against markdown files that have code in them. So it's running the code in the markdown files. And it's fascinating again to see how all of this automation, this project level automation comes together to try to close all those little gaps. Like I mentioned, the problem of a broken URL on my README. You could also have code that you had typed into a markdown file, and it turns out it doesn't work for whatever reason. Maybe it worked once something changed. This will run the code in your markdown files so that you know that it still works, which is great. Yeah, I'm all for more testing.

00:55:53 Yeah, well, even if you're not actually trying to execute it. And like, I'm asserting that my example returns seven, because maybe it says connect to a database and do other crazy stuff. It could at least be syntactically valid, right? It could look at and go, I loaded that up and I parsed that function and it didn't die. That's a start.

00:56:10 Exactly. There's levels of testing, and like you said, that it can get very complicated to do full testing of some kinds of code.

00:56:18 So how do you test your markdown? You read me down MD. Well, see, I fire up a series of a cluster of docker containers using docker compose, and then we can run the one example, and then it's good.

00:56:29 If there's a tool out there that launches missiles, I don't want to know how you're testing the code in your README.

00:56:35 Yeah, there's another one that is a little bit tough to test. One of the things that's interesting, by the way, this tool comes from Vincent Warmerdam, but it deals with multiple code blocks. So if you do the language specifier in markdown, so the triple back tick, you just say the word Python or JavaScript or C# or whatever, that will tell the formatters. Format. It like this, right? It's this type of syntax you should see. So if you do the Python one, it will run those, and it'll also do Bash as well, I believe. But what's interesting is you could have like and here's how you set it up, and then here's how you call it type of series of code blocks. And it will run all the code blocks. Or you can actually say, remember what you saw before, because that was the first half of what you need to.

00:57:23 Do the second half, right, because you're trying to tell a story. This is like a Jupyter notebook where you're interspersing code with commentary and then more code, and you need the multiple blocks of code to all be executed together or one after the other, you need the first one's results in the second one.

00:57:39 I certainly appreciate don't completely repeat yourself every time. In your code example, it would say you get started by importing this, and then you would create a class like this that derives from you wouldn't want to have to have import over and over, right? Yeah, this is cool. I don't use this one either, but it definitely looks like something I could see adopting. Now, here's something called Shed, which is not exactly what I want to talk about, but it's for formatting code. So it runs Autoflake, it runs Py, upgrade. You mentioned that before, I believe you can specify a version. Py upgrade me to Python 38, but not further, please.

00:58:17 Py Upgrade is good.

00:58:18 Yeah, it runs black. But what I do want to talk about is it runs Black in Docs.

00:58:24 Which formats the code in the Doc strings and in your docs, which again is one of those pairings of let's put this tool into that thing and have it do just a little bit.

00:58:35 This is super hard to get just right because you want to format code one of my markdown editors, if I highlight some code and I hit Shift tab to unindent it'll, put everything just to the left, I'm like, no, this is Python code. It has to have the space. You can't just put it on the left, like undo one level. Right. Things like that, where it's just like this is not quite formatted, right? Just running this, maybe even as a pre commit hook would be glorious. Just like all of my code in my examples, in my triplebactic, Python becomes blackened.

00:59:10 And if you're using Black, then you really want it everywhere. Right? You've given up control of the formatting of your code willingly. You see the value of it and you just want it everywhere. And this is great for getting it into your docs, too.

00:59:23 Exactly. There's gaps. Maybe your jupyter notebooks don't have Black formatter. Like, get it in there, get it into the docs, get it everywhere. Yeah. Getting ready.

00:59:30 Cool.

00:59:31 Okay, let's see this one.

00:59:34 Another person gave a shout out to your next project here. This is Yalamardi Said. Hey, we should check out Cog.

00:59:42 Yeah, cog is one of those tools that I wrote very long time ago to do one particular thing, and it ended up being useful in lots of other ways. Basically, Cog is a way that you can make a text file like a README MD and put little bits of Python in the middle of it. Not because you're trying to display that code to people, but because you want the results of that code to be part of your document.

01:00:05 A little bit like a Jinja, a template, maybe.

01:00:08 Exactly. But it's a little bit backwards because Jinja starts with the idea, well, it is like Jinja. Actually, I shouldn't say that it's just.

01:00:16 Like Jinja, but instead of being HTML, you want it to be text or something, right?

01:00:19 It can be anything you want. Jinja is particular to HTML in some ways, but Cog is completely agnostic. The bigger difference from Jinja with Cog is that the output of your code can go into the document. So that you process, you run the document, the output of your code becomes part of the document. So sort of the input file and the output file are the same file, so that you get sort of an item potent kind of processing of the file so you can have a README MD. You run cog on it. You still just have a reading me MD, but now you've got the results of the computation in the file. So, for instance, I use this in the coverage.py docs. There's a database schema for the SQL light data file that coverage Py writes that schema is in a string in a Python file someplace, but I also want it to be in my docs. So I use Cog in the Restructured text file to go and get the string from the Python code and splat it into the Restructured text file so that I know that the two are the same, because there's one source of truth and an automated process to bring it into the Restructured text file.

01:01:22 You know how they say there's like two hard problems in computer science? Naming things, cache and validation and off by one errors? Yes. I feel like maybe a fourth one should be identifying and controlling and keeping the one source of truth.

01:01:36 One source of truth is a big thing with me. All of these kinds of processes where you want to make it convenient to write information, but you also want to make it convenient to read information. And so you might want to publish information in more than one place. For instance, I mentioned that my change log is in a Rst file, but it also goes into GitHub releases because people want to read it in GitHub releases. So I get the information out of the change log and automatically publish it into GitHub releases. Yeah, cog has found a lot of use. Simon Willison has been very positive about Cog. He uses it in a number of places to keep his documentation up to date. I've used Cog to an extreme extent in my GitHub profile to, for instance, grab information from Pipi, where I mentioned what my projects are and things like that. Yeah, Cog is one of those things that started small, and it just has chugged along for a long time, and I continue to find more uses for it.

01:02:29 Yeah, that's great. Colin says using Cog logged to document CLI tools is Chef's Kiss.

01:02:35 Very nice.

01:02:37 We'll get into the end here. We're almost out of time, but luckily we're also almost out of things to talk about. We're not out of them, we're stopping.

01:02:45 There's a lot.

01:02:46 This is a small sampling, but here's one by hiding. That's awesome tools for the README profile. So this is a lot of let's do the test, click on their profile and see how it looks. You know what I mean? Yeah, got it. Got to get a little more in there. So this is more of a collection, but we have readmes for projects, but also read mes for humans. Right. You go to my account, you see a particular thing. Some people have really fancied that up with lots of things. And this project here talks about, well, what kind of cool stuff can you put on there that people might see. I haven't looked at yours recently. What's your profile look like?

01:03:22 So it's not as visual as this. It has a few badges, but I used Cog to, for instance, pull in the six most recent blog posts onto my page. I wanted to do recent tweets, but that was going to be hard because Twitter API wanted me to authenticate. And half the time I turn away when I'm asked to authenticate against the thing, because that's the hardest part of the whole thing. And it takes away all the fun.

01:03:46 Yeah.

01:03:47 The main thing I used Cog for, I used Cog on my README, and one of the things I did with it was to write Python code to generate that markdown syntax for badges and to put together Shields IO badge URLs. So both of those things are complicated, right? Shields IO is amazingly powerful, but how you actually put all the bits of information into the URL is hard to get. Right? And it's fiddly there's like ampersands and you have to quote them in the markdown regular expression. Yeah, it's just too intense. So I wrote Python functions to put together shields.io URLs. And then I called those Python functions from the Cog code in my README MD, and there's a GitHub action that runs the cog on it. Whenever I publish a blog post, my blog publishing triggers the GitHub action that recalcs my GitHub read me so that my latest blog post is on the top of the GitHub read me. Like I said, you can take this a long way. I might have gone too far with this.

01:04:44 No, I love it, but yeah, it's.

01:04:45 Cool to see how the tools can come together and you can automate all of these processes. Again, to go back to one source of truth. My blog is the one source of truth about what are my blog posts, but the information is also on my GitHub read me, because I thought that would be a useful thing for people to see when they look for me on GitHub.

01:05:04 Yeah, that's fantastic. All right, so this project here is like a whole host of things like that that you could do. And I love the use of cog and the GitHub actions just to chain it together.

01:05:16 Awesome tool for README profile. It's sort of like a Bling catalog. Like, you might want you might want to put this on your profile or put that on your profile.

01:05:24 If it was 1994 and you wanted a blank tag, here's a whole bunch of area, or a little animated diggy GIF. You could figure it out where this is like but so you get these graphs of like, what were your last year contributions over time, or when are you most likely to it's more badges.

01:05:41 Like, here's the latest blog posts, which is a thing that people can pull in if they don't want to do more of it themselves. How much time you spent coding in various languages per month or per week? Weekly here. That's pretty wild.

01:05:54 Yeah, he's got a lot of things here. Like what you're listening to on Spotify.

01:05:58 Yeah. Do they have emails? One of your coding activities? Because I spent a lot of time in email that I wish are you.

01:06:03 Typing code in your email? She's doing it wrong.

01:06:07 Just spending a lot of time in the email. I wish I didn't. Okay, so it's got what time of the day are you a morning person?

01:06:15 It has a snake game that goes around and raises like a centipede.

01:06:20 No, you're right. This is very reminiscent of the early GeoCities kind of internet where everything flashed and blinked and looked cool and had contrasting colors and stuff like that.

01:06:32 Yeah, we're only like a third of the way through this game.

01:06:36 They can give themselves trophies. They can give themselves I think this is stack overflow. Yeah, stack overflow reputation. There's just a ton of different stuff you can put together and I think it all comes back to besides maybe overdoing with digging animated Gifs and Bling tags. I think it comes back to your GitHub profile is a little bit like your resume. And how much can you say? More than just oh, I forked. Django.

01:07:00 Right. And the point of the profile is to let people know about you and hopefully they'll be interested in you in whatever way you want them to be interested. So all of these things that attract attention and you can choose something here that sort of has your vibe in whatever way. For instance, my page is very text heavy, but that's my vibe, that's the way I am. And if that's not for you, then you should look for someone else's profile. But if you want to know what I'm listening to on Spotify, then that's a thing to put on a profile page. So it's great. I mean, self expression is a wonderful thing and the fact that GitHub lets you build your own profile and that there are all these tools to do whatever you want with it, it's amazing.

01:07:41 It is amazing. All right, I think this is probably going to be it for our final thing to cover Read me and friends, let's close this out just really quickly with a give us the 70 story on coverage.py

01:07:56 That's a big deal. Alright, if you're going to make that big of a number, it might not.

01:07:59 Be a big deal. This is a tricky thing. So really what happened was I was looking through the bugs that people were reporting and a lot of them had to do with it. Couldn't find my source file where I said it should put the source file, and I was answering with, well, you have to do these tricky things in your configuration file and I thought maybe that should be simpler. So really the reason it's a 7.0 is because I made things better, but I also think you might have to change your settings in order for them to still work the way they used to work. So when you look at the change log for coverage 7.0, there's no amazing big thing. The biggest feature change is that when you get a text report out now, it can be in markdown format instead of in plain text format, and that's cool, but that's not like a 7.0 level feature. The real change is I think it's going to be better, but a few of you might have to update your settings. And I wanted to make it clear to people that that was going to happen, so I bumped the number to 7.0.

01:08:54 That seems totally reasonable and still going strong. It's beta one right now. When you foresee this becoming the pip install coverage sort of version, that's a great question.

01:09:05 I have to admit, to be perfectly honest with you, that I have been disappointed in the past at how few people try out betas. So I'm putting this out there in a disciplined way, and I'm trying to talk about it like, go and try the beta, but eventually I'm going to get tired of waiting for people, and I'm just going to publish it. And if the bug reports come in, then then we'll deal with them then, because there's only so much you can do to get people's attention on a beta.

01:09:29 Absolutely. I can totally understand that. All right, final two questions before you get out of here. Write some code with write some python code. What editor are you using these days?

01:09:37 Vim, Right on.

01:09:38 And I do not have any code completion plugins.

01:09:40 Okay.

01:09:40 I've said this before, I'm very low tech.

01:09:42 Perfect. And then notable pypi package. I kind of feel like we've covered a bunch, but is there anything you want to give a shout out?

01:09:48 We did cover a bunch. I've been very enamored of rich, I have to say. It's very cool. I'm looking forward to hearing more about what textual is going to be for building terminal UI interfaces for applications. But rich is astoundingly competent at what it tries to do.

01:10:05 Yeah. And what they're doing on the terminal is just nuts. It is nuts in a good way.

01:10:10 I only discovered just the other day, maybe people don't know this. That one of the rich styles. And this is a feature that terminals support, and rich is just tapping into it. But it gave a convenient way to do it. You can output text that's red or that's bold. You can output text that's a link where the word in the terminal is just click here, and behind it is the URL you told to have it, and then you can click the link in the terminal and go and visit things.

01:10:33 Astounding I'm familiar with terminals detecting links, but not having a different link text than the actual link. Right?

01:10:42 Yes. That's what I'm talking about. I didn't know it could do that.

01:10:45 Yeah, that's nuts.

01:10:46 Yeah, cool.

01:10:46 That's definitely a good one. All right, final call to action. People are thinking about their projects. I want to get started with some of these ideas. What do you tell them?

01:10:53 Think about your users, think about who you're writing for. And it's different people at different times and write words. I actually want to say one more thing. We talk about change logs as being really good for the users of your library. I find when I sit down to edit my change logs that I understand my own product better and that I think about the features I've built in a new way and sometimes actually go back and change them because in the process of trying to describe what happened, I learned something. Writing for readers is great writing. You will learn things when you write. Write more. It'll be good.

01:11:26 I can definitely see that you're like, I want to say, but it doesn't quite do this unless I change this other thing in code, and then it'll be true to what I wanted to say here. So, yeah, perfect.

01:11:36 Yes.

01:11:37 All right, Ned, thanks for coming back on the show. Great to have you here.

01:11:39 It's always fun.

01:11:40 Yeah. See you.

01:11:43 This has been another episode of Talk Python to me. Thank you to our sponsors. Be sure to check out what they're offering. It really helps support the show.

01:11:51 Listen to the local Maximum podcast. Learn about topics as diverse as the philosophy of probability and Elon Musk's next move. Just search for Local Maximum in your favorite podcast player.

01:12:03 Take some stress out of your life. Get notified immediately about errors and performance issues in your web or mobile applications with Sentry. Just visit Hawk Python Fm/sentry and get started for free. And be sure to use the promo code Talk Python all one word when you level up your Python. We have one of the largest catalogs of Python video courses over at Talk Python. Our content ranges from true beginners to deeply advanced topics like memory and Async. And best of all, there's not a subscription in sight. Check it out for yourself at training. Talk Python.FM be sure to subscribe to the show, open your favorite podcast app and search for Python. We should be right at the top. You can also find the itunes feed at /itunes, the Google Play feed at /Play and the direct RSS feed at RSS on Talk Python FM.

01:12:52 We're live streaming most of our recordings these days. If you want to be part of the show and have your comments featured on the air, be sure to subscribe to our YouTube channel at Talkpython.FM/YouTube. This is your host, Michael Kennedy. Thanks so much for listening. I really appreciate it. Now get out there and write some Python code.
