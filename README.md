## Intro
I recently discovered I could pick up some APRS packets with a really basic setup of just running ionosphere and a NoElec , and thought it'd be more useful to be able to view this in a website, rather than just looking at a stream of data in a console.

## Notes:
This document is still in progress, this is just the first draft I wanted to get saved.

I'm currently running two docker-compse stacks to do this, but ideally you'd run one containing all the services. If/when I get around to doing this, I'll share the combined compose file here
### Track Direct
APRS track direct needs to run on port 9000 for websockets and port 80 for the web interface.
Port 9000 clashes with Portainer, and port 80 will obviously clash with any local web servers already running.
You can probably get around this by running the stack on a secondary IP on your docker host, but I haven't worked this out yet.
A reverse proxy would also be ideal, but I haven't explored this at all.

Also, don't try and change the postgres db password in the docker-compose file, it's statically configured elsewhere.
### Direwolf
Direwolf uses a strange lat/long format, which seems to be similar to DMS, but I can't find it documented anywhere.
I've just dropped the decimal point in the seconds and that seems to work
example here:

        - LATITUDE=37^54.34992S 
          DMS format: 37° 54' 34.992'' S
        - LONGITUDE=145^24.49392E 
          DMS format: 145° 24' 49.392'' E
          
          



