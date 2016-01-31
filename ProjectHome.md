# Overview #
This library is based on Brett Hagman's Tone Generator lirary, we modify it and make it compatible with Arduino IDE 1.0x.
The main modifications is make it active low level and compatible with our buzzer electronic brick.

![ftp://imall.iteadstudio.com/Study_notes/Study_Notes_of_Iteaduino_Part_III_2.jpg](ftp://imall.iteadstudio.com/Study_notes/Study_Notes_of_Iteaduino_Part_III_2.jpg)

# Some functions in Tone library #

## makeTone.begin(speakerPin) ##
Function：to select to control pins of buzzer
Parameters：
	speakerPin : Pin N.O. for connecting to S port of buzzer

## makeTone.play(note) ##
Function：to let buzzer make a sound
Parameters：
note： value of certain note

## makeTone.stop() ##
Function：to stop making sounds

A song is composed of a number of notes, and a note corresponds to a frequency. If we know the corresponding frequency, and let Iteaduino output different frequencies to control the buzzer, the buzzer will make corresponding sounds. The relationship between different note and frequency is shown in the following three tables:

|ToneNote|1-|2-|3-|4-|5-|6-|7-|
|:-------|:-|:-|:-|:-|:-|:-|:-|
|A       |221|248|278|294|330|371|416|
|B       |248|278|294|330|371|416|467|
|C       |131|147|165|175|196|221|248|
|D       |147|165|175|196|221|248|278|
|E       |165|175|196|221|248|278|312|
|F       |175|196|221|234|262|294|330|
|G       |196|221|234|262|294|330|371|


# Demo #
```
#include <Tone_Itead.h>
int speakerPin = 3;
Tone makeTone;

// notes to play; see Tone_Itead.h for frequencies; 
int notes[] = { 
 NOTE_C4, NOTE_C4, NOTE_D4, NOTE_C4, NOTE_F4, NOTE_E4, 
 NOTE_C4, NOTE_C4, NOTE_D4, NOTE_C4, NOTE_G4, NOTE_F4,
 NOTE_C4, NOTE_C4, NOTE_C5, NOTE_A4, NOTE_F4, NOTE_E4, NOTE_D4,
 NOTE_AS4, NOTE_AS4, NOTE_A4, NOTE_F4, NOTE_G4, NOTE_F4}; 

// number of beats for each note
int beats[] = { 
 1, 1, 2, 2, 2, 4, 
 1, 1, 2, 2, 2, 4, 
 1, 1, 2, 2, 2, 2, 2, 
 1, 1, 2, 2, 2, 4}; 

// Calculate song length
int songLength = sizeof(notes) / sizeof(int); 
int tempo = 220; // in milliseconds

void playNote(int note, int beat){
 makeTone.stop(); // speaker reset
 makeTone.play(note); // play tone 
 delay(tempo * beat); // for specified number of beats
 makeTone.stop(); // speaker reset
 delay(tempo / 4); // pause between notes
}

void setup() {
 pinMode(speakerPin,OUTPUT);
 makeTone.begin(speakerPin); // set up piezo speaker
}

void loop() {
 for (int i = 0; i < songLength; i++) 
{
  playNote(notes[i],beats[i]); // make sound
}
  }

```

