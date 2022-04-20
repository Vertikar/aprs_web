## Intro
I recently discovered I could pick up some APRS packets with a really basic setup of just running ionosphere and a NoElec , and thought it'd be more useful to be able to view this in a website, rather than just looking at a stream of data in a console.

## Notes:
This document is still in progress.

This is currently setup to not transmit either via radio or IP into the APRS network.
To be able to transmit via IP into APRS-IS you need to have your amateur radio licence and a callsign assigned.

### Track Direct
APRS track direct needs to run on port 9000 for websockets and port 80 for the web interface.
Port 9000 clashes with Portainer, and port 80 will obviously clash with any local web servers already running.
You can probably get around this by running the stack on a secondary IP on your docker host, but I haven't worked this out yet.
A reverse proxy would also be ideal, but I haven't explored this at all.

Also, don't try and change the postgres db password in the docker-compose file, it's statically configured elsewhere.
### Direwolf
Direwolf uses a strange lat/long format, which seems to be similar to DMS, but I can't find it documented anywhere.
I've just dropped the decimal point in the seconds and that seems to work.

Example here:

        - LATITUDE=37^54.34992S 
          DMS format: 37° 54' 34.992'' S
        - LONGITUDE=145^24.49392E 
          DMS format: 145° 24' 49.392'' E
          
## Requirements
You'll need a half decent SDR, or you may need to work out your PPM.

I'm using a Nooelec NESDR Smart, which has a TCXO and I had no issues tuning to the Australia APRS VHF frequency with this. 

Some of the guides I read suggested you'd need to work out then specify your PPM, but the NESDR just worked.

## Usage
I've removed some environment items to an .env file

If you create .env file in the same directory as your docker-compose.yml and put in the below with the values relevant to you, you should be right to go.

```
CALLSIGN=<your callsign here> 
PASSCODE=-1
LATITUDE=37^54.34992S # replace with your lat - this is just to show the format used by direwolf.
LONGITUDE=145^24.49392E # replace with your long
```


