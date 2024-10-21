![alt text](https://assets.juce.com/juce/JUCE_banner_github.png "JUCE")

JUCE is an open-source cross-platform C++ application framework for creating
desktop and mobile applications, including VST, VST3, AU, AUv3, AAX and LV2
audio plug-ins and plug-in hosts. JUCE can be easily integrated with existing
projects via CMake, or can be used as a project generation tool via the
[Projucer](#the-projucer), which supports exporting projects for Xcode (macOS
and iOS), Visual Studio, Android Studio, and Linux Makefiles as well as
containing a source code editor.

## Getting Started

The JUCE repository contains a
[master](https://github.com/juce-framework/JUCE/tree/master) and
[develop](https://github.com/juce-framework/JUCE/tree/develop) branch. The
develop branch contains the latest bug fixes and features and is periodically
merged into the master branch in stable [tagged
releases](https://github.com/juce-framework/JUCE/releases) (the latest release
containing pre-built binaries can be also downloaded from the [JUCE
website](https://juce.com/get-juce)).

JUCE projects can be managed with either the Projucer (JUCE's own
project-configuration tool) or with CMake.

### CMake

Version 3.22 or higher is required. To use CMake, you will need to install it,
either from your system package manager or from the [official download
page](https://cmake.org/download/). 

# JUCECMAKE a la rachelle

- clone JUCE in GitHubDesktop
`https://github.com/juce-framework/JUCE`

- [JUCE CMAKE documentation](https://github.com/juce-framework/JUCE/blob/master/docs/CMake%20API.md)

- see also 'juce_cmake_vscode_example-main` in this folder for a template formatted to VS

- clone Analog Tape Model in GitHubDesktop: 
`https://github.com/jatinchowdhury18/AnalogTapeModel`

- cd into the repository

- Initialize submodules:

```bash
git submodule update --init --recursive
```

- Generate the builds with CMake:

```bash
cd Plugin

cmake -Bbuild -DCMAKE_BUILD_TYPE=Release
cmake --build build/ --config Release
```


