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

### Hardware

You can run this python app on a Raspberry PI 3B, 4 or 5 or on any Linux (Ubuntu 22.04 tested). 

You need:
* Python 3
* fluidsynth               sudo apt install fluidsynth
* flask                    pip install Flask
  
### Python code
