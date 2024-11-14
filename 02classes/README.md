## compound data types review

## classes review

## SC CPP FWIW

# Ooops! = Object Oriented Programming + Classes

*by [Rui Pereira](http://www.rux-werx-here.net/)*


## Overview
This tutorial is a quick and practical introduction to Object-Oriented Programming in openFrameworks and a how-to guide to build and use your own classes.
By the end of this chapter, you should understand how to create your own objects and have a lot of balls bouncing on your screen!

![balls screenshot](images/balls_screenshot.png "balls screenshot")

## What is Object Oriented Programming
Object-Oriented Programming (OOP) is a programming paradigm based on the use of objects and their interactions. A recurring analogy is to see a "class" as a cookie cutter that can create many cookies, the "objects".
Some terms and definitions used within OOP are listed below:

- A class defines the characteristics of a thing - the object - and its behaviors; it defines not only its properties and attributes but also what it can do.

- An object is an instance of a class.

- The methods are the object's abilities.

## How to build your own Classes (simple Class)
Classes and objects are the fundamental part of Object Oriented programming.
Because of cooking, like coding, is fun and we tend to experiment in the kitchen let's continue with the classic metaphor of a cookie cutter as a class, defining its interactions, capabilities and affordances, and cookies as the objects.
Every class has two files: a header file, also known as declarations file with the termination '.h' and an implementation file, terminating in '.cpp'.
A very easy way of knowing what these two files do is to think of the header file (.h) as a recipe, a list of the main ingredients of your cookie. The implementation file (.cpp) is what we're going to do with them, how you mix and work them to be the perfect cookie!
So let's see how it works:

First of all, let's create the two class files: `Ball.h` and `Ball.cpp` and place these in the project's `src` folder.

Declare a class in the header file (.h). In this case, the file name should be `Ball.h`.
Follow the code below and type into your own `Ball.h` file, please note the comments I've included to guide you along.

```cpp
#ifndef _BALL // if this class hasn't been defined, the program can define it
#define _BALL // by using this if statement you prevent the class to be called more than once which would confuse the compiler
#include "ofMain.h" // we need to include this to have a reference to the openFrameworks framework
class Ball {

    public: // place public functions or variables declarations here

    // methods, equivalent to specific functions of your class objects
    void setup();    // setup method, use this to setup your object's initial state
    void update();  // update method, used to refresh your objects properties
    void draw();    // draw method, this where you'll do the object's drawing

    // variables
    float x;        // position
    float y;
    float speedY;   // speed and direction
    float speedX;
    int dim;        // size
    ofColor color;  // color using ofColor type

    Ball();  // constructor - used to initialize an object, if no properties are passed the program sets them to the default value
    private: // place private functions or variables declarations here
}; // don't forget the semicolon!
#endif
```

We have declared the Ball class header file (the list of ingredients) and now let's get to the cooking part to see what these ingredients can do!
Please notice the '#include' tag. This is a way to tell the [compiler](http://www.cplusplus.com/doc/tutorial/introduction/ "Compiler introduction on cplusplus.com") ([wikipedia](https://en.wikipedia.org/wiki/Compiler "Wikipedia on compilers")) about any files to include in the implementation file. When the program is compiled these '#include' tags will be replaced by the original file they're referring to.
The 'if statement' (#ifndef) is a way to prevent the repetition of header files which could easily occur. This is called an [include guard](https://en.wikipedia.org/wiki/Include_guard "Wikipedia on include guards"). Using this pattern helps the compiler to only include the file once and avoid repetition. Don't worry about this now, we'll talk about it later on!

We will now create a class for a ball object. This ball will have color, speed and direction properties: it will move across the screen and bounce against the wall. Some of these properties we will create with randomized attributes but we'll be careful to create the right logic for its motion behaviors.

Here's how you can write the class `Ball.cpp` file, the implementation file:

```cpp
#include "Ball.h"
Ball::Ball(){
}

void Ball::setup(){
    x = ofRandom(0, ofGetWidth());      // give some random positioning
    y = ofRandom(0, ofGetHeight());

    speedX = ofRandom(-1, 1);           // and random speed and direction
    speedY = ofRandom(-1, 1);

    dim = 20;

    color.set(ofRandom(255),ofRandom(255),ofRandom(255)); // one way of defining digital color is by addressing its 3 components individually (Red, Green, Blue) in a value from 0-255, in this example we're setting each to a random value
}

void Ball::update(){
    if(x < 0 ){
        x = 0;
        speedX *= -1;
    } else if(x > ofGetWidth()){
        x = ofGetWidth();
        speedX *= -1;
    }

    if(y < 0 ){
        y = 0;
        speedY *= -1;
    } else if(y > ofGetHeight()){
        y = ofGetHeight();
        speedY *= -1;
    }

    x+=speedX;
    y+=speedY;
}

void Ball::draw(){
    ofSetColor(color);
    ofDrawCircle(x, y, dim);
}
```

Now, this is such a simple program that we could have written it inside our ofApp(.h and .cpp) files and that would make sense if we didn't want to reuse this code elsewhere. One of the advantages of Object Oriented Programming is reuse. Imagine we want to create thousands of these balls. The code could easily get messy without OOP. By creating our own class we can later re-create as many objects as we need from it and just call the appropriate methods when needed keeping our code clean and efficient. In a more pragmatic example think of creating a class for each of your user-interface (UI) elements (button, slider, etc) and how easy it would be to then deploy them in your program but also to include and reuse them in future programs.


## Make an Object from your Class
Now that we've created a class let's make the real object! In your ofApp.h (header file) we'll have to declare a new object but first, we need to include (or give the instructions to do so) your Ball class in our program. To do this we need to write:

```cpp
#include "Ball.h"
```

on the top of your ofApp.h file. Then we can finally declare an instance of the class in our program. Add the following line inside the `ofApp` class, just above the final "};".

```cpp
Ball myBall;
```

Now let's get that ball bouncing on screen! Go to your project ofApp.cpp (implementation) file. Now that we've created the object, we just need to set it up and then update its values and draw it by calling its methods.

In the `setup()` function of ofApp.cpp add the following code:

```cpp
myBall.setup(); // calling the object's setup method
```

In the `update()` function add:

```cpp
myBall.update(); // calling the object's update method
```

and in the `draw()` function lets add:

```cpp
myBall.draw(); // call the draw method to draw the object
```

Compile and run! At this point, you should be seeing a bouncing ball on the screen! Great!

## Make objects from your Class

By now, you're probably asking yourself why you went to so much trouble to create a bouncing ball. You could have done this (and probably have) without using classes. In fact, one of the advantages of using classes is to be able to create multiple individual objects with the same characteristics. So, let's do that now! Go back to your ofApp.h file and create a couple of new objects:

```cpp
Ball myBall1;
Ball myBall2;
Ball myBall3;
```

In the implementation file (ofApp.cpp), call the corresponding methods for each of the objects
in the ofApp's `setup()` function:

```cpp
myBall1.setup();
myBall2.setup();
myBall3.setup();
```

in the ofApp's `update()` function:

```cpp
myBall1.update();
myBall2.update();
myBall3.update();
```

and also in the `draw()` function:

```cpp
myBall1.draw();
myBall2.draw();
myBall3.draw();
```

## Make more Objects from your Class
We've just created 3 objects but you can have already see how tedious it would be to create 10, 100 or maybe 1000's of them. Hard-coding them one by one would be a long and painful process that could be easily solved by automating the object creation and function calls. Just by using a couple for loops we'll make this process simpler and cleaner. Instead of declaring a list of objects one by one, we'll create an array of objects of type `Ball`. We'll also introduce another new element: a constant. Constants are set after any #includes as #define CONSTANT_NAME value. This is a way of setting a value that won't ever change in the program.
In the ofApp class header file, where you define the balls objects, you also define the constant that we'll use for the number of objects:

```cpp
#define NBALLS 10
```

We'll now use the constant NBALLS value to define the size of our array of objects:

```cpp
Ball groupOfBalls[NBALLS];
```

An array is an indexed list of items of the same type. The index is used to access a particular item in the list. This index usually starts with 0, so the first `Ball` (object) is found at groupOfBalls[0]. Only a handful of programming languages start the index of an array with 1. If you try to access an invalid index (either larger than the size of the array or a negative one), you get an error. Check the 'C++ basics' chapter for more information on arrays. In our implementation file, we create an array of objects and call their methods through 'for' loops.

In the `setup()` function remove:

```cpp
myBall1.setup();
myBall2.setup();
myBall3.setup();
```

and add

```cpp
for(int i=0; i<NBALLS; i++){
    groupOfBalls[i].setup();
}
```

instead.

In the `update()` function remove

```cpp
myBall1.update();
myBall2.update();
myBall3.update();
```

and write

```cpp
for(int i=0; i<NBALLS; i++){
    groupOfBalls[i].update();
}
```

In the `draw()` function replace

```cpp
myBall1.draw();
myBall2.draw();
myBall3.draw();
```

with

```cpp
for(int i=0; i<NBALLS; i++){
    groupOfBalls[i].draw();
}
```

By using the for loop, the `setup()`, the `update()` and the `draw()` method is called for each `Ball` object in the `myBall`-array and no object has to be touched manually.


## Make even more Objects from your Class: properties and constructors

As we've seen, each of the objects has a set of properties defined by its variables (position, speed, direction, and dimension). Another advantage of object-oriented programming is that the objects created can have different values for each of their properties. For us to have better control of each object, we can have a method that allows us to define these characteristics and lets us access them. Because we want to do this right after creating the object, let's do this in the method called `setup()`.  We will modify it to pass in some of the properties of the object, let's say its position and dimension. First, let's do this in the Ball definitions file (*.h):

```cpp
void setup(float _x, float _y, int _dim);
```

We'll need to update the Ball implementation (*.cpp) file to reflect these changes.

```cpp
void Ball::setup(float _x, float _y, int _dim){
    x = _x;
    y = _y;
    dim = _dim;

    speedX = ofRandom(-1, 1);
    speedY = ofRandom(-1, 1);
}
```

Your `Ball.cpp` file should look like this by now:

```cpp
#include "Ball.h"

Ball::Ball(){
};

void Ball::setup(float _x, float _y, int _dim){
    x = _x;
    y = _y;
    dim = _dim;

    speedX = ofRandom(-1, 1);
    speedY = ofRandom(-1, 1);

    color.set(ofRandom(255), ofRandom(255), ofRandom(255));
}

void Ball::update(){
    if(x < 0 ){
        x = 0;
        speedX *= -1;
    } else if(x > ofGetWidth()){
        x = ofGetWidth();
    speedX *= -1;
    }

    if(y < 0 ){
        y = 0;
        speedY *= -1;
    } else if(y > ofGetHeight()){
        y = ofGetHeight();
        speedY *= -1;
    }

    x+=speedX;
    y+=speedY;
}

void Ball::draw(){
    ofSetColor(color);
    ofDrawCircle(x, y, dim);
}
```

Now in the ofApp.cpp file we will need to run this newly implemented method right when we start our application so it will reflect the different settings on each object as they are created. So, in the `ofApp::setup()`

```cpp
for(int i=0; i<NBALLS; i++){

    int size = (i+1) * 10; // defining the size of each ball based on its place in the array
    int randomX = ofRandom( 0, ofGetWidth() ); //generate a random value bigger than 0 and smaller than our application screen width
    int randomY = ofRandom( 0, ofGetHeight() ); //generate a random value bigger than 0 and smaller than our application screen height

    groupOfBalls[i].setup(randomX, randomY, size);
}
```