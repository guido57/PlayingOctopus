# PlayingOctopus
 
## Overview 

I got the idea watching the traditional wind-chimes and guessing how they could be played automatically.
Here you'll find all the software necessary to playing Octopus, while the hardware project is here: https://hackaday.io/project/195138-playing-octopus

![](https://github.com/guido57/PlayingOctopus/blob/main/docs/Octopus.png)

The main distinctive capabilities of this building are:
1) It can play 1 selectable track of any MIDI file by the 6 tubular bells
2) the whole tune (all the MIDI tracks) is played by the loudspeaker
3) the software, by a web interface, allows to:
   * search the MIDI file from thousands of songs
   * select the track to be played by the octopus
   * tune the mallet movements (target, rest, speed)

## Software Architecture

![](https://github.com/guido57/PlayingOctopus/blob/main/docs/BlockDiagram.png)
 
## Python Flask Server

ESP32 is very powerful but its storage memory (flash) is very limited while we need to play mp3 (1 - 4 MBytes) along with midi files, therefore we need an external storage server.

### Hardware and libraries

You can run this python app on a Raspberry PI 3B, 4 or 5 or on any Linux (Ubuntu 22.04 tested). 

You need:
* Python 3
* fluidsynth
```
sudo apt install fluidsynth
```

* flask
```
pip install Flask
```
  
### Server code

The pages served by the flask python server are:

* /events?query=<word_to_search_separated_by_a_+>   e.g. /search?q=rolling+stones
  return a list of songs accomplishing the query
  
* /tracks?index=<codefile>  e.g. /tracks?index=63118
  return the tracks for that filecode (song id)

* /get_mp3?index=<codefile>  e.g. /get_mp3?index=63118
  convert the mid file (e.g. 63118.mid) to an mp3 file (e.g. 63118.mp3) and store it to the server folder "static"

* /output.mp3?query=<codefile>  e.g. /output.mp3?query=63118
  stream that mp3 file (e.g. 63118.mp3) to the client 

* /output.mid?query=<codefile>  e.g. /output.mid?query=63118
  stream that mid file (e.g. 63118.mid) to the client 



