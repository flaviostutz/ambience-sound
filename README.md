# ambience-sound
Stuff for my home ambience sound system.
Basic sound manager is a RaspberryPi with Docker containers installed.

## Installation

### Software
* Install the latest version of Hypriot on a RaspberryPi
  * Download the latest version from https://blog.hypriot.com/downloads/
  * Copy the image to the SD card using Etcher
  * Raspberry 2 is enough for Spotify Connect
* Install ALSA packages
  * apt-get update && apt-get install alsa-tools alsa-utils rpi-update
* Configure ALSA to use your USB card as default device (ignore the trashy onboard sound card, hehe)
  * echo "blacklist snd_bcm2835" > /etc/modprobe.d/alsa-blacklist.conf
  * echo "options snd-usb-audio index=0" > /etc/modprobe.d/alsa-base.conf

### Hardware
* Connect a good USB sound card
  * I use a Behringer UCA 202 USB card and do like its sound
  * I've already tested various 2-3 dollars eBay USB Sound cards and most of them are OK for "normal" people
* Install amplifier and ceiling speakers
  * JBL round ceiling speakers and car sound amplifiers deliver great results
    * Single Corzus HF 404 (4 channel x 50wrms@4ohm) with 8 x JBL Selenium Speaker 6FR2R
    * Each channel drives two speakers (8 ohm each) in parallel, resulting 4ohm per channel@50wrms (speaker and amplifier are just enough)

### Spotify
* Create docker-compose.yml
```yml
version: "3.3"
services:
  rpi-spotify:
    image: flaviostutz/rpi-spotify:1.5.0
    network_mode: host
    restart: always
    devices:
      - /dev/snd:/dev/snd
    environment:
      - SPOTIFY_NAME=Kitchen
      - EQUALIZATION=rock
```
* Run ```docker-compose up -d```
* Open your Spotify with Premium account and click on "Connect to device". 
* "Kitchen" or whatever you set should appear on Spotify. Choose it and the music will start playing on your speakers (hopefully!). 
* For more info, check http://github.com/flaviostutz/rpi-spotify
