---
layout: post
title: "Raspberry Pi - Camera and Motion"
---

<!---
Markdown cheatsheet: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
--->

<!---
deploy jekyll preview: jekyll serve --detach --port $PORT --host $IP
--->

<!--- Post text follows --->

Today I'm going to (finally) get the camera on my Raspberry Pi functioning. One of our cats happens to be a Large Adult Son yet goes on some very loud sprint exercises a few times a day. We'd like to catch him in the act.

**Equipment**:
* Raspberry Pi 2 Model B v1.1
* Raspberry Pi Camera v2.1
* CanaKit USB Wi-Fi Adapter

I've had this Pi sitting around for awhile; a few weeks ago I wiped the SD card and started over with Raspbian Stretch.

#### 1. Set up and configure Pi

1. Forget your login information for the Pi. Spend awhile trying to guess it, then pull the SD card and start searching the house for a microSD adapter. Realize you wrote yourself a note when you set up Stretch in November (thanks Evernote). Successfully ssh into the Pi.
2. Set up a static IP address:
    * Set via ifconfig: `ifconfig wlan0 10.0.1.101 netmask 255.255.255.0 up`

3. Reconnect to the pi. Do apt-get update, apt-get upgrade because who knows who long it's been.
    * Many downloads failed due to "101: Network is unreachable" errors to several mirrors. Let's cross our fingers.

#### 2. Set up Motion

1. I installed Motion back in November, so it's time to review and verify the ~/.motion/motion.conf file.
    * daemon on: start in daemon mode and release terminal
    * width 1280, height 960: set capture resolution
    * target_dir /tmp/motion: location to save image files
    * stream_auth_method 1: use basic authentication (username/password)
    * stream_authentication <username>:<password>: set some credentials so the camera isn't live to anyone on our network
2. Start Motion:
    * Use ~/.motion/motion.conf; have to use sudo or the daemon will not be able to create the various log/storage directories. **TO DO:** Fix this in the future via setting correct permissions.
    * Motion will stream the content at port 8081, and run a simple web config panel at 8080. We set authentication information for these above, but it's not particularly secure. This will only point at the hallway for a little bit as an experiment, so that's sufficient for now.
3. Stop Motion:
    * Sometimes sudo service motion stop works; most reliable:
{% highlight shell %}
pi@raspberrypi:~ $ cat /var/run/motion/motion.pid 
2208
pi@raspberrypi:~ $ sudo kill -9 2208
{% endhighlight %}
