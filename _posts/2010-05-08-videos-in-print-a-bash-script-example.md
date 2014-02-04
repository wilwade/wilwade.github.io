---
layout: post
title: "Videos in Print: A Bash Script Example"
description: ""
category: code
tags: [bash]
---
{% include JB/setup %}

One of the best things about Linux/Unix is the ability to automate through the [BASH](http://www.gnu.org/software/bash/) scripting. If you are not familiar with Bash then I suggest you Google something like Bash tutorials. I suggest that you skip over the technical parts, and focus on what I used Bash to accomplish.

I am currently working on typesetting our family blog so that we can have a paper version for the future, and just a way to flip through pre-commented photos. On our blog however, we have many videos.  Until someone comes up with a slightly more inexpensive and usable method of paper video, it is rather difficult to print videos. So I thought that perhaps a film strip of sorts would help "replace" the video and give some transformation from film to print.  However we are talking about 30+ videos.  I do not have the time to go through and manually extract frames and then put them together.  So I wondered if I could automate the process.

Using [mplayey](http://www.mplayerhq.hu) to output the frames to png, I was able to then automatically put them into a grid using [ImageMagick](http://www.imagemagick.org). In the end it was rather easy.

[Gist Script!](https://gist.github.com/wilwade/8534145)

>Note: You really should never run a shell script you download from the internet without first at least reading over it a little to make sure it is not going to wipe your drive or anything.  This will not do that, but it is always good to remember.

Anyway the script is fairly simple.  Most of the length is from a little bit of error checking and default setting.  There is likely easier ways to do this, but I did it the way I did and you can feel free to rewrite it.  Basically it is really just to commands.  One is the mplayer command to extract the frames as pngs, the other is the ImageMagick command, montage, to create the strip.

To use the command you can do something as simple as feed it a video file.  The default is to create a 5 by 5 grid (see the example below), but you can pass it other parameters.

For those with little experience with Bash a parameter is something that comes after the command.

command parameter1 parameter2 ... parameterN

For this script the parameters are as follows:

1. The video file name
2. The number of frames wide for the strip to be
3. The number of frames tall for the strip to be
4. The width of each frame
5. The height of each frame

(The frame aspect ratio is preserved.  White is added for fill.)

Note that in order to get frames that were evenly spaced I needed to spit all the frames out to png first.  There are some ways around this, but most people have more space than they know what to do with.  This does mean that it is really only effective for shorter clips.

> @TODO Jan 20, 2014 It is possible to do this better with ffmpeg, but I have not yet updated the script.

Here is an example.  This is a video of an April fools joke on my in-laws.  We "left" our daughter on their doorstep.  Note that this is the best example, as it has the most visual action.  The process does not work as well for audio centered videos.

![Surprise]({{ site.url }}/assets/2010/4_1_aprilfools2.AVI.png)