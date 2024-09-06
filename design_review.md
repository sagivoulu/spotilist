# Spotilist

## Background
As a social dancer, I want to play music from my phone when social dancing with friends.
My current problem is that I have a large selection of dancing music, but no easy way to select the appropriate songs to the current situation (Slow, fast, hip hop, blues etc...)

Usually Social dancing DJs use a tool called [VirtualDj](https://www.virtualdj.com/) to tag their songs and create dynamic playlists, but that requires playing music from a laptop which is way more effort than just hooking up my phone to spotify.

The goal of this tool is to bridge this gap, allowing me to create dynamic playlists in spotify based on tags that are assigned to each song (Either manually assigned or automatically)

## Features description
Spotilist is a simple script that will
1. Scan a given songs list for tags
2. Will create spotify playlists of these songs based on the song tags and given conditions.

   For example:
   1. `80 <= bpm <= 90 and energy = "low"` - `late night music`
   2. `110 <= bpm <= 120 and genre = "blues"` - `fast blues`
   
## Usage story
The user will:
1. Download a list of songs to their computer using [spotdl](https://github.com/spotDL/spotify-downloader.git) or any other tool for downloading music.
2. Tag the downloaded lists using [VirtualDj](https://www.virtualdj.com/) or any other tool. The tags will be saved inside the songs mp3 data.
3. Define a set of playlist rules (currently inside the script) alongside playlist names
4. Run the `Spotilist` script, which will create / update a playlist for each rule, adding all the songs that match that given rule

## Architecture - high level design

The tool will receive as input:
1. Master spotify playlist - This is the master playlist all songs are in.
2. Local music directory - A local directory with tagged mp3 songs.
3. List of playlist rules - Rules & names for the target playlists.
4. Spotify credentials - Used to create & update spotify playlists.

## Current limitations
In order to keep this project quick I set up the following limitations:
1. I don't handle downloading & tagging songs, use other tools for that
2. Only songs that are in the `Master spotify playlist` will be used by the script, so if a song is not there it will be ignored
3. Songs in spotify will be matched to their mp3 file by song title + artist as close as possible
