System V init script template
=============================

Ubuntu and debian service registration. It executes on boot, provides start|stop|restart apis. 

Tutorial here: http://stackoverflow.com/questions/7221757/run-automatically-program-on-startup-under-linux-ubuntu

sudo mv /filename /etc/init.d/
sudo chmod +x /etc/init.d/filename 
sudo update-rc.d filename defaults 
Script should now start on boot. Note that this method also works with both hard links and symbolic links (ln).

Edit

At this point in the boot process PATH isn't set yet, so it is critical that absolute paths are used throughout. BUT, as pointed out in the comments by Steve HHH, explicitly declaring the full file path (/etc/init.d/filename) for the update-rc.d command is not valid in most versions of Linux. Per the manpage for update-rc.d, the second parameter is a script located in /etc/init.d/*. Updated above code to reflect this.

Another Edit

Also as pointed out in the comments (by Charles Brandt), /filename should be an init style script. A good template was also provided - https://github.com/fhd/init-script-template.

Another link to another article just to avoid possible link rot (although it would be saddening if GitHub died) - http://www.linux.com/learn/tutorials/442412-managing-linux-daemons-with-init-scripts

A simple template for init scripts that provide the start, stop,
restart and status commands.

Handy for [Node.js](http://http://nodejs.org/) apps and everything
else that runs itself.

Getting started
---------------

Copy _template_ to /etc/init.d and rename it to something
meaningful. Then edit the script and enter that name after _Provides:_
(between _### BEGIN INIT INFO_ and _### END INIT INFO_).

Now set the following three variables in the script:

### dir ###

The working directory of your process.

### user ###

The user that should execute the command.

### cmd ###

The command line to start the process.

Here's an example for an app called
[algorithms](http://algorithms.ubercode.de):

    dir="/var/apps/algorithms"
    user="node"
    cmd="node server.js"

Script usage
------------

### Start ###

Starts the app.

    /etc/init.d/algorithms start

### Stop ###

Stops the app.

    /etc/init.d/algorithms stop

### Restart ###

Restarts the app.

    /etc/init.d/algorithms restart

### Status ###

Tells you whether the app is running. Exits with _0_ if it is and _1_
otherwise.

    /etc/init.d/algorithms status

Logging
-------

By default, standard output goes to _/var/log/scriptname.log_ and
error output to _/var/log/scriptname.err_. If you're not happy with
that, change the variables `stdout_log` and `stderr_log`.

License
-------

Copyright (C) 2012-2014 Felix H. Dahlke

This is open source software, licensed under the MIT License. See the
file LICENSE for details.
