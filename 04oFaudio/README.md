# audio-reactivity with FFT
- based on [Lewis Lepton oF tutorials 047 + 048](https://github.com/lewislepton/openFrameworksTutorialSeries)

# Shape
## Project Generator
- name
- path correct?
- Addons:
  - `ofxGui`
- Platform
- Template:
  -`Visual Studio Code`
- Make Project!

## Find a short .wav file on your computer!
- add it to the `bin/data` folder in the `src` for your project

## Setup
- go to source>ofApp.h
- under `#include "ofMain.h"` add:
`#include "ofxGui.h"`
- below last 'void' message:
```
ofxPanel gui;
ofParameter<float> audioamplitude;
ofParameter<float> visualdecay;

ofSoundPlayer sound;

float * fft;
float * soundSpectrum;
int bands;
```
- go to source>ofApp.cpp
- in `void ofApp::setup` function add:
```  
sound.load("YOURFILENAMEHERE.wav");
sound.play();
sound.setLoop(true);

gui.setup();
gui.add(audioamplitude.set("audioamplitude", 0.5, 0.0, 1.0));
gui.add(visualdecay.set("visualdecay", 0.5, 0.0, 1.0));

fft = new float[128];
for (int i = 0; i < 128; i++){
  fft[i] = 0;
}
bands = 64;

```
- in `void ofApp::update` function add:
```
ofSoundUpdate();

sound.setVolume(audioamplitude);
soundSpectrum = ofSoundGetSpectrum(bands);
for (int i = 0; i < bands; i++){
  fft[i] *= visualdecay;
  if (fft[i] < soundSpectrum[i]){
    fft[i] = soundSpectrum[i];
  }
}
```
- in `void ofApp::draw` function add:
```
for (int i = 0; i < bands; i++){
  ofDrawCircle(ofGetWidth()/2, ofGetHeight()/2, fft[i]*100);
}
gui.draw();
```
# Run oF from Terminal!
- cd to project folder
- `make`
- `make RunRelease`

# Polylines
## Project Generator
- name
- path correct?
- Addons:
  - `ofxGui`
- Platform
- Template:
  -`Visual Studio Code`
- Make Project!

## Find a short .wav file on your computer!
- add it to the `bin/data` folder in the `src` for your project

## Setup
- go to source>ofApp.h
- below last 'void' message:
```
  ofSoundPlayer sound;
  
  float * fft;
  float * soundSpectrum;
  int bands;
```
- go to source>ofApp.cpp
- in `void ofApp::setup` function add:
```  
sound.load("YOURFILENAMEHERE.wav");
sound.play();
sound.setLoop(true);

fft = new float[512];
 for (int i = 0; i < 512; i++) {
  fft[i] = 0;
}
bands = 512;

```
- in `void ofApp::update` function add:
```
  ofSoundUpdate();
  
  soundSpectrum = ofSoundGetSpectrum(bands);
  for (int i = 0; i < bands; i++) {
    fft[i] *= 0.9;
    if (fft[i] < soundSpectrum[i]) {
      fft[i] = soundSpectrum[i];
    }
  }
```
- in `void ofApp::draw` function add:
```
 ofTranslate(256, 192);
 for (int i = 0; i < bands; i+=16) {
   ofPolyline polyline;
   for (int j = 0; j < bands; j++) {
     polyline.addVertex(j, i - fft[j] * 100.0);
   }
   polyline.draw();
  }
```
# Run oF from Terminal!
- cd to project folder
- `make`
- `make RunRelease`
