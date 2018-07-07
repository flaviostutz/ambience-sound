# ambience-sound
Stuff for my home ambience sound system.
Basic sound manager is a RaspberryPi with Docker containers installed.

## Installation
### Preparation of RaspberryPi
* Install the latest version of Hypriot
* Connect a USB sound card

### Spotify
* run
```
docker run -d --restart=always --name=rpi-spotify -e SPOTIFY_NAME="Kitchen" --device /dev/snd:/dev/snd --net=host svanscho
/rpi-spotify
```

## Usage
* Open your Spotify with Premium account and click on "Connect to device". "Kitchen" or whatever you set should appear on Spotify. Click and the music will start playing. 
