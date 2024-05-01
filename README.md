# Crystal-widgets

 Crystal-widgets is a set of system monitoring widgets for the Übersicht application suitable for both Apple Silicon and Intel-based Macs. Please note however that on some entry-level older Intel Macs these widgets may put a rather heavy load on the cpu. In those cases, it may be advisable to adjust the update times in some of the widgets.
The screenshot below is from a MacStudio M1 Ultra.

![Screenshot of crystal-widgets](https://github.com/locupleto/crystal-widgets/blob/main/Screenshot.png?raw=true)

## Description

The `crystal-widgets` collection of widgets primarily focused on system performance monitoring, designed to enhance your desktop experience. These widgets provide real-time information on your system's performance, including CPU usage, memory consumption, and a basic system profile. The design is minimalist with a glass-like aesthetic, contributing both functionality and visual appeal to your desktop.

The core monitoring functionality leverages a custom build of the performance monitor `htop`. Binaries for both Intel and Apple Silicon architectures are included in the widget package. If you prefer to build these binaries yourself, you can find the necessary resources at [crystal-htop](https://github.com/locupleto/crystal-htop).

Please note that even if you have the original `htop` installed, you must use the custom-built binary `crystal-htop` included with these widgets for them to work. The only difference between htop and crystal-htop is that crystal-htop logs performance metrics in real-time to small text files in a temporary directory. These files are then read and displayed by the widgets. The `crystal_htop_runner.sh` script will ensure that only one single instance of `crystal-htop` will run, and it will operate in a headless mode using the screen command to remain hidden.

## Installation preparations

To install the `crystal-widgets`, follow these steps:

- Ensure that Übersicht is installed on your macOS system. If not, you can download it from [Übersicht's official website](http://tracesof.net/uebersicht/).
- Ensure that Homebrew is installed on your system for managing software packages. If it's not installed, follow the instructions at [Homebrew's official website](https://brew.sh/).
- Before installing `crystal-widgets`, ensure you have the necessary tools installed. Run the following commands in your terminal to check for them and install them if they are missing:

```bash
command -v flock >/dev/null 2>&1 || brew install flock
```
- Then install node and use it to install wikit to get the system-profiler widget to work:

```bash
command -v node >/dev/null 2>&1 || brew install node
command -v wikit >/dev/null 2>&1 || npm install -g wikit
```

- Download the [zip-file](https://github.com/locupleto/crystal-widgets/blob/main/crystal-widgets.zip) containing all widgets and the helper files needed. Unzip the folder. This will unpack to a folder named put_into_widgets_folder. The contents of that folder should look like this:

```bash
.
├── crystal-analog-clock.widget
│   └── index.coffee
├── crystal-calendar.widget
│   ├── index.coffee
│   └── widget_runner.sh
├── crystal-htop-cpu-bar.widget
│   ├── index.coffee
│   └── widget_runner.sh
├── crystal-htop-load.widget
│   ├── index.coffee
│   └── widget_runner.sh
├── crystal-htop-mem-bar.widget
│   ├── index.coffee
│   └── widget_runner.sh
├── crystal-htop-swap-bar.widget
│   ├── index.coffee
│   └── widget_runner.sh
├── crystal-system-profiler.widget
│   ├── index.coffee
│   ├── macOS_name.sh
│   └── widget_script.sh
├── crystal-top-cpu.widget
│   └── index.coffee
├── crystal-top-mem.widget
│   └── index.coffee
├── crystal_common.sh
├── crystal_htop_arm64
├── crystal_htop_runner.sh
└── crystal_htop_x86
```

## Configuration

Before you can run the Übersicht application with the crystal widgets you need to configure the `crystal_common.sh` file in the folder by appending the full path of the two command tools you just installed. Depending on your system the installation paths of these may vary. 

- Open the terminal, change directory so that you are in the same directory as the  `crystal_common.sh` file.

- Then append the full path to `flock` and `wikit` commands as they are installed in your system to the end of the `crystal_common.sh` file like this:

```bash
echo "export FLOCK_CMD=$(which flock)" >> crystal_common.sh
echo "export WIKIT_CMD=$(which wikit)" >> crystal_common.sh
```

## Authorize executables

The final step necessary in order to run the scripts and two binaries in the widget set is to delete the com.apple.quarantine attribute of these files. Please make sure that you are in the widget directory when you issue the command. If you are uncertain of what you are doing, please read up on what this command does before you run it. One way to avoid doing this is to instead build the appropriate binary yourself. As previously stated, you can find the necessary resources for doing so here: [crystal-htop](https://github.com/locupleto/crystal-htop).

Otherwise simply execute these two one-liners with your admin-password:

```bash
sudo xattr -d com.apple.quarantine crystal_htop_arm64
sudo xattr -d com.apple.quarantine crystal_htop_x86
```

You should now be able to test the binary from the terminal like this (on an Apple Silicon Mac):

```bash
./crystal_htop_arm64
```

which should show a display similar to this:
![Screenshot of crystal_htop](https://github.com/locupleto/crystal-widgets/blob/main/Screenshot_htop.png?raw=true)
And if with the crystal-htop binary running you should see a nnumber of small text-files with the performance measurements that this command logs continously and is subsequently used by the widgets.

```bash
ls -l /tmp
```

The only thing left to do now is to move all files in the folder to the Übersichts widget folder which you can see and also change in the settings of the Übersicht application.

Start the Übersicht application and hopefully your widgets should appear on your desktop if you have followed all the instructions.

## Optional customization

If you like you can check out the `crystal_common.sh` file and experiment with customizing the colors of the performance bars in the widgets. Also if you don't like any of the widgets just remove them from the widgets folder. Just make sure to keep the three files `crystal_common.sh`, `crystal_htop_runner.sh` and `crystal_htop_x86` or `crystal_htop_arm64` depending on the CPU-architecture pf your Mac.

