# review

## compound data types

## classes

# [PureData](https://puredata.info/)
- open my osctest.pd file in this folder
- sending MIDI and OSC concurrently...

# receiving OSC in oF
- make project with oFxosc addon
- go to source>ofApp.h
- under `#include "ofMain.h"` add:
`#include "ofxOsc.h"`
- below last 'void' message:

`	ofxOscSender sender;
	ofxOscReceiver receiver;

	float oscx = 0.0;
	float oscy = 0.0; `

- go to source>ofApp.cpp
- in `void ofApp::setup` function add:
`  sender.setup("localhost", 12345);
  receiver.setup(12345);`
- in `void ofApp::update` function add:
`  while(receiver.hasWaitingMessages()){
    ofxOscMessage msg;
    receiver.getNextMessage(msg);
    if (msg.getAddress() == "/x"){
      oscx = msg.getArgAsFloat(0);
    }
    if (msg.getAddress() == "/y"){
      oscy = msg.getArgAsFloat(0);
    }
  }
`
- in `void ofApp::draw` function add:
`  ofDrawCircle(oscx+100, oscy+100, 100);`