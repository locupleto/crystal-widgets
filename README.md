# crystal-widgets

A set of system monitoring widgets for the Übersicht application.

# Description

`crystal-widgets` is a collection of widgets primarily focused on system performance monitoring, designed to enhance your desktop experience. These widgets provide real-time information on your system's performance, including CPU usage, memory consumption, and a basic system profile. The design is minimalist with a glass-like aesthetic, contributing both functionality and visual appeal to your desktop.

The core monitoring functionality leverages a custom build of the performance monitor `htop`. Binaries for both Intel and Apple Silicon architectures are included in the widget package. If you prefer to build these binaries yourself, you can find the necessary resources at [crystal-htop](https://github.com/locupleto/crystal-htop).

## Installation

To install the `crystal-widgets`, follow these steps:

- Ensure that Übersicht is installed on your macOS system. If not, you can download it from [Übersicht's official website](http://tracesof.net/uebersicht/).
- Ensure that Homebrew is installed on your system for managing software packages. If it's not installed, follow the instructions at [Homebrew's official website](https://brew.sh/).
- Before installing `crystal-widgets`, ensure you have the necessary tools installed. Run the following commands in your terminal:

```bash
brew install flock
brew install wikit
```bash
- Download the zip-file containing all widgets and the additional files needed to male them work into the Übersicht widget folder