# XVFB-AWS-Selenium:   Steps to set up XVFB screen for AWS-Selenium headless test execution. XVFB will help view live tests on local machine using a VNC Server.




sudo apt-get update
sudo apt-get install ubuntu-desktop
sudo apt-get install vnc4server
apt-get install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal

vncserver

Add password: P@ssword1

vncserver -kill :1

vim /home/usernamehere/.vnc/xstartup

replace everything and paste: 

#!/bin/sh

export XKL_XMODMAP_DISABLE=1
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS

[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup [ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
vncconfig -iconic &

gnome-panel &
gnome-settings-daemon &
metacity &
nautilus &
gnome-terminal &

org: [ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup


Do: vim ~/.vnc/xstartup and verify it is replaced. If not, do it again.

Exit.

Reconnect to server with: ssh -L 5901:localhost:5901 qa_user@ipAddress
Instead of ssh qa_user@qa_user@ipAddress

5901 is vncserver port number. We are tunnelling port number as AWS is configured to accept only port 22

Open VNC viewer on local machine and connect to: localhost:5901
Password: P@ssword1

If display is logging into display#2, do netstat -tnlp and kill all related pids
And delete log files cd ~/.vnc/
And delete rm /tmp/.X1-lock

				******

References: https://stackoverflow.com/questions/25657596/how-to-set-up-gui-on-amazon-ec2-ubuntu-server

https://www.youtube.com/watch?v=9BAoJ7JZHr0&t=550s


https://linuxize.com/post/how-to-save-file-in-vim-quit-editor/

https://blog.codeenigma.com/using-vnc-as-the-display-manager-to-run-selenium-tests-e4f817137ce2

https://gist.github.com/alonisser/11192482


PS:
VNC password set is Password_89
Using command: x11vnc -storepasswd

