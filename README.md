# gnome-screensaver-lock
GNOME Screensaver Fails to Lock with VirtualBox Running - This is my solution

More details on the problem are here: http://mikeb.org/2016/02/06/gnome-screensaver/

The solution included here should be installed in /usr/lib/systemd/system-sleep/ and is confirmed to work with VirtualBox blocking gnome-screensaver in Fedora 23.

When the laptop is put to sleep, the script will be ran from that directory and perform the following:

- Look for the logged in user's gnome-session PID so it can extract environment information
- Extract the DBUS_SESSION_BUS_ADDRESS socket so that gnome-screensaver-command can communicate with gnome-screensaver
- Identify the username of the user so commands can be ran as the unprivileged user
- Check if the screensaver is running
- If it is not, it will grab the first non-VirtualBox window it can find and change focus to it
- If there are not non-VirtualBox windows it will change focus to the desktop with the "show desktop" functionality
- Finally, it will lock the screen with gnome-screensaver
