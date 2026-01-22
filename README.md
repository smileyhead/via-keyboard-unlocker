# via-keyboard-unlocker
A simple script to temporarily unlock VIA-compatible keyboards for configuration on Linux.

Attempting to configure a VIA-compatible keyboard on https://usevia.app/ might net you the following errors:
> NotAllowedError: Failed to open the device.
> 
> Received invalid protocol version from device

This script attempts to remedy this by implementing the solution discussed in [this thread](https://bbs.archlinux.org/viewtopic.php?id=285709) into a nice and simple bash script, so that you don't have to do manual investigative work every time you want to configure your keyboard.

# How It Works
The script works by…
* asking the user to unplug their keyboard;
* taking a snapshot of the `/dev` directory;
* asking the user to plug their keyboard back in;
* and taking another snapshot of the `/dev` directory.

By doing this, the script should be able to automatically figure the exact device ID(s) the system assigned the keyboard. After this, the script will change the file permissions to allow the VIA configuration tool to access the keyboard, while the script keeps waiting.

Before any file modifications are made, the script displays its findings in the terminal and asks for confirmation to avoid modifying unwanted files.

After configuration has concluded, the user may pass `done` (or just `d`) to the script to initiate the re-locking process.
