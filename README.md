# MusicPlayer

The MusicPlayer Arduino library provides an easy way to play a simple melody over one of the Arduino's PWM output pins. It also defines constants for all notes from C2 to C6.

### Usage:
  1.  Make one array containing the frequencies of all the notes of the song (the note constants declared in MusicPlayer.cpp are useful here), and one containing the duration of all notes.
  	(Durations are given in fractions of a quarter note, i.e. half note = 2, eigth note = 1/2, and so on.)
  2.  Make a new MusicPlayer object with the constructor MusicPlayer(pin, tempo, pauseLength, song, toneLengths, songLength):
    - pin: The pin to output the song over. (Must support PWM).
    - tempo: The tempo of the song (in BPM, beats per minute)
    - pauseLength: If non-zero, adds a duration of silence between each note, which helps separate the notes when several of the same note are played in succession. In fraction of a quarter note; should be quite small.
    - song: The array of note frequencies.
    - toneLengths: The array with the duration of each note (in fractions of a quarter note).
    - songLength: The amount of notes in the song. Corresponds to length of song and toneLengths arrays.
  3.  Call tick(deltaTime) in a loop. deltaTime is the amount of time since the last call, measured in milliseconds.



## MusicXMLParser

Provides a convenient way to make the arrays required by the MusicPlayer library, by parsing the standardized MusicXML format.
This can be output by different scoring software. MuseScore (http://musescore.org) is a good, free alternative.

To use, simply run the parser.py script and provide the path to your MusicXML file and a path to save the produced file to.
Then copy the arrays from the resulting file.

**IMPORTANT**: As the arduino tone function can only play one tone at a time, the parser assumes that there's only one note at a 
time in the MusicXML file. If there are points with several notes played simultaneously, e.g. chords, these will be mapped
one after the other by the parser, which will produce another result than expected. In other words, make sure that the score
never plays more than one note at a time.
