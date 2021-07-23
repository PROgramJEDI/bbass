🔊 an asynchronous music downloader to make your life‬ easy.

## Overview
🔊BASS is a simple tool that provides the functionality of downloading and managing songs using existing advanced tools. In addition, we provide a simple console-interface to allow anyone who wants's to download their favorite song easily. 

## Installation
In order to install 🔊BASS (BubbleBASS / bbass) you first have to set up Python and the PIP package manager. Then write the following command correspondingly to your operating system:

* Windows: ```pip install bbass```
* Linux: ```pip3 install bbass```

🎉 Congratulations you installed 🔊BASS. If you want to know how to use it continue to the following guiding sections.

## Getting Started
In order to use 🔊BASS, we'll have to import it to our program first. In addition, we'll import asyncio to download songs to our local storage:
```python
>>> import asyncio
>>> from bbass import Folder, Song, Playlist
```
Currently 🔊BASS consist of two base classes: Folder and Song. While the Folder class is responsible to manage all of the bookmarks general folders, the Song class mostly include properties of a song. Let's create a new Song object and give it a custom link from YouTube:
```python
>>> song = Song(name='Toto - Africa (Official Music Video)', 
		link='https://www.youtube.com/watch?v=FTQbiNvZqaY')
>>> song.id
FTQbiNvZqaY
>>> song.command
cd "/home/***/***/***/Library/bbass/bbass" && youtube-dl https://www.youtube.com/watch?v=FTQbiNvZqaY --extract-audio --audio-format "mp3" --audio-quality 0 -o "%(title)s.%(ext)s"
>>> asyncio.run(song.download())
```
Pretty simple, right. However, it's frustrating to copy-paste the name of the song, each time we want to download one (I think that too). In order to let ourselves be lazier, we can use the Playlist class. In order to create a meaningful playlist, we better initialize it with an existing and unique folder name:
```python
>>> play = Playlist('Songs')
>>> play.songs # returns all of the unique youtube songs in the playlist
<generator object Playlist.songs at 0x7f0678ebddd0>
```
The .song attribute is a generator of Song objects, if there are any songs in the given folder. In order to get all the song objects in one shot, we need to convert the generator to a non-iterator:
```python
>>> list(play.songs)
[<bass.Song object at 0x7fbc260b8f40>, <bass.Song object at 0x7fbc260b8ca0>, <bass.Song object at 0x7fbc24e6f250>, <bass.Song object at 0x7fbc24e6f2b0>, <bass.Song object at 0x7fbc24e6f2e0>]
```
Each object in this list is a Song object, therefore, we can easily access each Song's properties. However, if you just want to see the links, commands, names, or IDs of all the songs in the playlist, then 🔊BASS will do it for you:
```python
>>> list(play.links)
['https://www.youtube.com/watch?v=SP9wms6oEMo', 'https://www.youtube.com/watch?v=FTQbiNvZqaY', ...]
>>> list(play.names)
['George Harrison - My Sweet Lord (Official Audio)', 'Toto - Africa (Official Music Video)', ...]
>>> list(play.commands)
['cd "/home/***/***/***/Library/bbass/bbass" && youtube-dl https://www.youtube.com/watch?v=SP9wms6oEMo --extract-audio --audio-format "mp3" --audio-quality 0 -o "%(title)s.%(ext)s"', ...]
>>> list(play.ids)
['SP9wms6oEMo', 'FTQbiNvZqaY', 'oG6fayQBm9w', ...]
```
Let me show you how to download as many songs as you want, in a click of a button (and asynchronously):
```python
>>> import asyncio
>>> play = Playlist('Songs') # folder name should be unique!
>>> asyncio.run(play.download()) # the same as we did with class Song...
```
Wow 🔊BASS just downloaded all of the YouTube songs you had in the folder - simple, useful, and amazing tool. Pay attention that the songs were downloaded to the folder the program ran in. You can even download songs to a custom path - just add the path as a first parameter in the download function. The good thing is that 🔊BASS creates a database to manage which songs were downloaded and which were not.

## Advanced Usage
