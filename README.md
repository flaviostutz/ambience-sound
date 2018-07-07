# ambience-sound
Stuff for my home ambience sound system.
Basic sound manager is a RaspberryPi with Docker containers installed.

## Installation

### Software
* Install the latest version of Hypriot on a RaspberryPi
  * Download the latest version from https://blog.hypriot.com/downloads/
  * Copy the image to the SD card using Etcher
  * Raspberry 1 is enough for Spotify Connect (uses ~25% CPU)
* Install ALSA packages
  * apt-get update && apt-get install alsa-tools alsa-utils rpi-update
* Configure ALSA to use your USB card as default device (ignore the trashy onboard sound card, hehe)
  * echo "options snd-usb-audio index=0" > /etc/modprobe.d/alsa-base.conf
  * paste into /etc/asound.conf
```
pcm.!default {
    type hw
    card 0
}

ctl.!default {
    type hw
    card 0
}
```

### Hardware
* Connect a good USB sound card
  * Three dollars eBay cards doesn't have good low and high frequencies, but are OK for simple sound sets. 
  * I use a Behringer UCA 202 USB card and do like its sound
* Install amplifier and ceiling speakers
  * JBL round ceiling speakers and car sound amplifiers deliver great results
    * Single Corzus HF 404 (4 channel x 50wrms@4ohm) with 8 x JBL Selenium Speaker 6FR2R
    * Each channel drives two speakers (8 ohm each) in parallel, resulting 4ohm per channel@50wrms (speaker and amplifier are just enough)

### Spotify
* run
```
docker run -d --restart=always --name=rpi-spotify -e SPOTIFY_NAME="Kitchen" --device /dev/snd:/dev/snd --net=host svanscho
/rpi-spotify
```
* usage
  * Open your Spotify with Premium account and click on "Connect to device". 
  * "Kitchen" or whatever you set should appear on Spotify. Choose it and the music will start playing on your speakers (hopefully!). 
