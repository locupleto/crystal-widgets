# Crystal-widgets

 Crystal-widgets is a set of system monitoring widgets for the Übersicht application suitable for both Apple Silicon and Intel-based Macs.
![Screenshot of crystal-widgets](https://github.com/locupleto/crystal-widgets/blob/main/Screenshot.png?raw=true)

# Description

The `crystal-widgets` collection of widgets primarily focused on system performance monitoring, designed to enhance your desktop experience. These widgets provide real-time information on your system's performance, including CPU usage, memory consumption, and a basic system profile. The design is minimalist with a glass-like aesthetic, contributing both functionality and visual appeal to your desktop.

The core monitoring functionality leverages a custom build of the performance monitor `htop`. Binaries for both Intel and Apple Silicon architectures are included in the widget package. If you prefer to build these binaries yourself, you can find the necessary resources at [crystal-htop](https://github.com/locupleto/crystal-htop).

Please note that even if you have the original htop installed, you must use the custom-built binary crystal-htop included with these widgets for them to work. The only difference between htop and crystal-htop is that crystal-htop logs performance metrics in real-time to small text files in a temporary directory. These files are then read and displayed by the widgets. Only a single instance of crystal-htop will run, and it will operate in a headless mode using the screen command to remain hidden.

## Installation

To install the `crystal-widgets`, follow these steps:

- Ensure that Übersicht is installed on your macOS system. If not, you can download it from [Übersicht's official website](http://tracesof.net/uebersicht/).
- Ensure that Homebrew is installed on your system for managing software packages. If it's not installed, follow the instructions at [Homebrew's official website](https://brew.sh/).
- Before installing `crystal-widgets`, ensure you have the necessary tools installed. Run the following commands in your terminal:

```bash
brew install flock
brew install wikit
```
- Download the [zip-file](https://github.com/locupleto/crystal-widgets/blob/main/crystal-widgets.zip) containing all widgets and the helper files needed and move them into the Übersicht widget folder.

## Customization

Check out the crystal_common.sh file if you want to experiment with customizing the colors of the performance bars in the widgets.

