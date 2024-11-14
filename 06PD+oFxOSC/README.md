# review

# [PureData](https://puredata.info/)
- open my osctest.pd file in this folder
- sending MIDI and OSC concurrently
- toggle on and connect!

# open in Logic, Live, Any DAW!

## Project Generator
- name
- path correct?
- Addons:
  - `ofxOSC`
- Platform
- Template: `Visual Studio Code`
- Generate!
- go to src>ofApp.h
- under `#include "ofMain.h"` add:
`#include "ofxOsc.h"`
- below last 'void' message:
```
ofxOscSender sender;
ofxOscReceiver receiver;

float oscx = 0.0;
float oscy = 0.0; 
```
- go to src>ofApp.cpp
- in `void ofApp::setup` function add:
```  
sender.setup("localhost", 12345);
receiver.setup(12345);
```
- in `void ofApp::update` function add:
``` 
while(receiver.hasWaitingMessages()){
    ofxOscMessage msg;
    receiver.getNextMessage(msg);
    if (msg.getAddress() == "/x"){
      oscx = msg.getArgAsFloat(0);
    }
    if (msg.getAddress() == "/y"){
      oscy = msg.getArgAsFloat(0);
    }
  }
```
- in `void ofApp::draw` function add:

`  ofDrawCircle(oscx+100, oscy+100, 100);`

# Run oF from Terminal!
- cd to project folder
- `make`
- `make RunRelease`

## pd 16 step double sequencer

## More on PD? Simon Hutchinson PD tutorials on YouTube (I know...)