# Simple Pi Calendar
A simple dashboard that shows two calendar views (by day and agenda), a traffic map, the weather, and a picture of your choosing. This was a reaction to my previous efforts with Magic Mirror, which is a fantastic app, but is completely overbuilt for probably 95% of the implementations. Also MagicMirror runs a bit slow on the pi zero.

Simple Pi Calendar on the other hand is just an HTML page that you load up in a chromium browser on your pi. This was quick project, but it works. I did pull out all the config values though, so it's not a total mess.

<img src="/example_picture.jpg" height="550px">

# Software
The runs well on any computer from the most underpowered (pi zero) to your laptop. It's built to be loaded without a webserver, just open the page in a browser (once you've set up the config of course). If you are using it on a pi it's worthwhile to set it up to launch the browser at startup and preload the page.

The calendars make use of a library called [FullCalendar](https://fullcalendar.io/). In order to get it to properly reload the calendar on a recurring basis, the whole page reloads every 30 minutes. 

# Hardware
This expects to be run on a widescreen monitor turned on its side. The dimensions are hardcoded into the html right now. But you can go in there and modify them to suit your needs.

# Setup
You will need to make your own config file `config/config.js`, there is an example file to help
```
cp config/config.js.example config/config.js
vi config/config.js
# edit away
```

If you want something other than the cheezy default image, place a file in the directory with the name `image.png`. If you need it to be another type, you'll have to update the source


## Google API Keys Required
In order to setup that file you will have to create API keys for Google Calendar and Google Maps. This is pretty easy, but does require a google account. Here are some simple [straightforward instructions](https://docs.simplecalendar.io/google-api-key/) on getting an API key. Follow the same steps to get a Maps key as well - you'll want a key for the Google Maps Javascript API.

## Get Your Pi Booting Right
Install unclutter to make the mouse disappear when not in use, this might require a reboot to take effect

```sudo apt-get install unclutter```

Modify your autostart

```vi ~/.config/lxsession/LXDE-pi/autostart```

Here is my version, it also stops screen blanking and the pointer from showing up:
```
@lxpanel --profile LXDE-pi
@pcmanfm --desktop --profile LXDE-pi
@point-rpi
@xset s off
@xset -dpms
@xset s noblank
@unclutter -idle 0
@chromium-browser --incognito --kiosk http://127.0.0.1
```

Now you just need to setup a basic webserver to serve the index.html file in he root of this repo
try this if you need help with that: https://www.raspberrypi.org/documentation/remote-access/web-server/apache.md

Pro tip: If you are sshed into the pi and still want to be able to launch chromium to test, you can use this:

```DISPLAY=:0 /usr/lib/chromium-browser/chromium-browser --disable-quic --enable-fast-unload --enable-tcp-fast-open --disable-gpu-compositing --enable-pinch --incognito --kiosk http://127.0.0.1```


## Some things to work on
- Emoji Support: Figure out how to get the pi to display cute emoji's when you put them in your calendar entries. I did find [this article](https://www.omgubuntu.co.uk/2016/08/enable-color-emoji-linux-google-chrome-noto), but that didn't resolve things for me. If I do sort it out, it would likely need to be a script that you run on the pi, since it's an OS or browser level change
- Dynamic resolution support: to get things to look nice I hardcoded the dimensions. Math could likely be used to get this looking good without hardcoding, but that was beyond the scope of my kitchen display.
- More efficient Calendar Reload: take another stab at getting calendars to refresh without reloading the whole page, which is a bit jarring on a pi zero
