# simple_pi_calendar
A very simple dashboard to display on a raspberry pi type dashboard that shows two calendar views, a traffic map, the weather, and a picture of your choosing.

[[/example_picture.jpg|alt=a picture of a dashboard in the wild]]

# Setup
You will need to make your own config file `config/config.js`, there is an example file to help
```
cp config/config.js.example config/config.js
vi config/config.js
# edit away
```

## You'll need keys
In order to setup that file you will have to create API keys for Google Calendar and Google Maps. This is pretty easy, but does require a google account. Here are some simple [straightforward instructions](https://docs.simplecalendar.io/google-api-key/) on getting an API key. Follow the same steps to get a Maps key as well - you'll want a key for the Google Maps Javascript API.



## Some things to work on
Figure out how to get the pi to display cute emoji's when you put them in your calendar entries.
  I haven't had much of any success with this, but it's a start
https://www.omgubuntu.co.uk/2016/08/enable-color-emoji-linux-google-chrome-noto
- it would likely need to be a script that you run
