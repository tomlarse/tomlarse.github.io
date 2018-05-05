---
layout: post
title: Producing Skype Meeting Broadcast for webinars and webcasts
date: 2015-12-01 14:04
author: tomlarse
comments: true
categories: [E5, General, Office 365, Skype for Business, Skype for Business Online, Skype Meeting Broadcast, Unified Communications, video conferencing]
---
The last couple of months Skype Meeting Broadcast has been available in technical preview and we've been testing it as a platform to deliver webinars and webcasts on a couple of occations. This post is a writeup on our experiences from this.
<h1>Scheduling and set up</h1>
This process is fairly straight-forward. If your tenant has Skype Meeting Broadcast enabled, you log in to <a href="https://broadcast.skype.com/" target="_blank">https://broadcast.skype.com/</a> with your Office 365 credentials and you are good to go

The first screen that you are presented with is a calendar that neatly displays all your scheduled broadcasts, and where you can schedule new meetings

<img class="alignnone size-full wp-image-668" src="https://codesalot.files.wordpress.com/2015/12/2015-12-01_13-27-55.png" alt="2015-12-01_13-27-55" width="1039" height="954" />

If you click "New Meeting" you will be taken to the create meeting page where you can set the name, time and duration of the meeting. You will also be able to create an event staff and choose what kind of audience will be able to join the broadcast. For webinars all of these could possibly be used, we have most often used it with the Anonymous setting.

<img class="alignnone size-full wp-image-674" src="https://codesalot.files.wordpress.com/2015/12/2015-12-01_13-21-56.png" alt="2015-12-01_13-21-56" width="1039" height="954" />

The duration can be set to a maximum of 4 hours, but we've been having casts extend that with almost double that time without issue.

After the initial set ut you are presented with an overwiew page that can also be accessed by clicking the meeting in the dashboard overview. Here you can get the link to the broadcast and also create an outlook invitation for the broadcast. You are also able to customize the broadcast from here.

<img class="alignnone size-full wp-image-681" src="https://codesalot.files.wordpress.com/2015/12/2015-12-01_13-36-35.png" alt="2015-12-01_13-36-35" width="1039" height="954" />

Currently "customizing" means that you can add two modules to the broadcast page, one in the sidebar and one below the broadcast. As of writing this post, two options are available as content to these modules:
<ul>
	<li>Add discussion from a Yammer page</li>
	<li>Bing Pulse integration</li>
</ul>
I haven't played with <a href="www.bingpulse.com" target="_blank">Bing Pulse</a> at all, so I don't really know what it can do, but the Yammer integration has been really useful and adds a real time feedback mechanism to a one way communication scenario. You need to create a group in a Yammer network that all participants can access to be able to use it, so information about this should be included in the invite, so the participants have time to prepare for this before the webcast.
<h1>Broadcast Startup</h1>
Prior to the broadcast start, event staff should join the meeting and get set up by starting video and uploading content to the broadcast. The event staff could consist of both presenters and producers in the meeting, but what we have found to be the best is to only have producers as staff and join the presenters to the meeting as a normal Skype meeting participant, more on that later.

The meeting join link is found on the meeting summary page and the link is used by both staff and participants

<img class="alignnone size-full wp-image-700" src="https://codesalot.files.wordpress.com/2015/12/2015-12-01_13-47-37.png" alt="2015-12-01_13-47-37" width="1039" height="572" />

Staff click the Sign in as event team member button. The Skype for Business client will start up as normal and staff joins the broadcast as a normal Skype meeting, but with some small differences in the user interface. Once joined and a powerpoint is uploaded this is what it looks like:

<img class="alignnone size-full wp-image-707" src="https://codesalot.files.wordpress.com/2015/12/2015-12-01_13-57-22.png" alt="2015-12-01_13-57-22" width="1278" height="755" />

Those familiar with the meeting UI will notice a couple of new buttons next to the presentation. This is where you control the broadcast and layout of the screen. Once an active video is selected, you are able to start the broadcast and select between the following layouts
<ul>
	<li>Video Only</li>
	<li>Video and Content</li>
	<li>Content only</li>
</ul>
These layouts can be switched between throughout the broadcast and can be used by the producers to break up the broadcast a bit. They shouldn't be switched between too often, but is a nice way to add some flavour to the broadcast. The "Video and Content" layout will display the presentation with the video in a small picture on the right side of the broadcast feed.

One thing to be aware of, once the broadcast has started all sound in the meeting will be broadcast as well, so this meeting should not be used to communicate between producers and presenters. IM's will not be displayed, so that should be the preferred method of communicating behind the scenes.

Also, once the broadcast has started it can not be stopped again without ending the entire broadcast. Do not use the Stop Broadcast button to pause the broadcast!

After the broadcast has ended a recording will be available on the meeting link, provided the "Enable meeting video recording" checkbox was checked during meeting set up.

With this we've covered the basics of producing a Skype Meeting Broadcast, but this leaves a couple of things to be desired.
<h1>Producers and presenters</h1>
it is fully possible to be both a presenter and a producer in a meeting, but often a presenter will not have the technical ability to produce their own meeting and in those cases it might not even be a good idea to give them the opportunity. Once one staffmember has joined the broadcast meeting it is fully possible to join presenters to the meeting as in a normal Skype meetin, either via drag and drop or via the meeting entry info which will contain a normal meeting join link to the meeting. This is not the same as the broadcast meeting join link.

If presenters join this way, you are able to select them as main video for the broadcast, and they will be able to present content to the meeting, but they will not be able to control starting and stopping the brodcast and will not have access to the layout controls. We have found this to be a very good solutions in cases where you want to separate production and content presentation.

What we also have found in these cases is that it is a very good idea to have at least two participants with producing capabilities in the meeting at all times, in case one of them drops out of the meeting. This can happen for various reasons, but the most common are network issues or computer crashes.
<h1>Advanced content sharing</h1>
The only possible content to present in a broadcast is a powerpoint presentation. No other content that the Skype for Business client normally can present is available to broadcast. There is also a limitation in that only one video source can be broadcast at the same time, gallery view can not be broadcast.

To work around this I've been using <a href="https://www.xsplit.com/">XSplit Broadcaster</a> which is a software that will take a lot of input sources, for instance media files, desktop areas, youtube videos etc and is able to in real-time create a video stream to a virtual webcam that can be used to send video in to a Skype meeting. In this way we can sow together our own layout for the content presentation and providing a lot more options for the content in the presentation. The entire layout is sent to the meeting as one video stream and uses the "Video Only" layout in Broadcast Meeting.

The only issue with Xsplit is that the virtual webcam that comes with it uses Direct Media to display the image, and the Skype for Business client only supports Windows Media Foundation. This means that the windows desktop client is not able to read from this virtual webcam. The workaround for this has been to join the meeting from the web app client in a Chrome browser. Chrome can access Direct Media devices, and can in that way send the video created by XSplit in to the meeting broadcast.

This has enabled us to use broadcast meeting with some advanced features, amongst others:
<ul>
	<li>Display video from all presenters on top of the presented content</li>
	<li>Display live demos from the desktop</li>
	<li>Send prerecorded video in to the broadcast</li>
	<li>Live drawing on top of a presentation</li>
	<li>Setting up a pause screen with countdown to when the broadcast will resume</li>
</ul>
And so on.

Using XSplit and Broadcast meeting together, we've made some really professional looking webinars. In one case for instance, I used teamviewer to capture the desktops of the presenters and with XSplit i combined those with both their videos and sent them to the meeting in several different layouts depending on the situation. This enabled me to produce a meeting from one computer where me and the two presenters all where separated by great distances physically. If we'd been in the same room, it would also be possible to use different pro-grade cameras as well, in stead of the webcams.

I am certain that there exists other kinds of software that does the same as XSplit as well, please let me know about them!
<h1>Concluding tips</h1>
<ul>
	<li>Always be more than one producer, or at least as producer have two computers joined to the meeting as staff, preferably on two separate internet connections if the broadcast is important.</li>
	<li>Prepare. Always prepare all aspects of the entire event well in advance
<ul>
	<li> Will we use Yammer or Bing Pulse?
<ul>
	<li>Accounts need to be set up and participants need information about joining</li>
</ul>
</li>
	<li>What kind of content do we need?
<ul>
	<li>Is it enough with only Powerpoints as shared content?</li>
</ul>
</li>
	<li>Producers should have access to agenda and content in advance to create a plan for layouts and layout switching, especially if using anything other than pure powerpoint presentations.</li>
</ul>
</li>
	<li>Never ever press the "Stop Broadcast" button unless the broadcast is fully completed.</li>
	<li>Familiarize yourself with the platform before you start producing broadcasts. Run several test broadcasts.</li>
</ul>
