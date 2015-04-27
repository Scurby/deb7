# deb7
SWGEmu Development Environment setup for Debian 7 OS

﻿VirtualBox, VMWare, or native install. Edit as needed. 
	VirtualBox - https://www.virtualbox.org/wiki/Downloads
	I used:
	
	8g mem
	32g virtual drive
	max cores
	bridged network

=============================
# Install Debian 7 

https://www.debian.org/distrib/

	(net install) 64 bit 
	Should work on any debian package distro
****************
	username=swgemu  
	password=123456
	root pw=12345678

*TODO - make configurable username and pass - $USER and $PWD*
****************
Predefined software selections - Default selection

	(*)Debian Desktop
	(*)Print Server
	(*)Standard System Utilities
****************
Config sudoer as needed

Run all CLI commands as sudo with user 'swgemu'. 
https://www.digitalocean.com/community/tutorials/how-to-add-delete-and-grant-sudo-privileges-to-users-on-a-debian-vps
****************
Run Updates
sudo apt-get update

# Import scripts # - do this in perms?

Copy '/folder/files' into home folder

	/home/bin/ - place all shell scripts here - set as read/write/executable
	TODO - Be sure that is executable:
	chmod +x /path/to/script - # perms

	/home/run/conf/ - place run_gdb in /home/run/
	- /conf/ should be empty.

	/home/setup - place eclipse tarball and Egit-prop tarball here

=====================
# Restart

*TODO force restart??? # perms*

RESTART!!!

=====================
# Run setup scripts

The following shell scripts can be run from the command line. They are numbered in the order I use them.

1. options - Installs Optional packages

	- xclip 
	- terminator 
	- vim 
	- chromium 
	- quassel
	- TODO fix dropbox install
        
2. first - Installs required packages and programs

	- gcc, g++, git, gdb, automake, make, libreadline-gplv2-dev
	- libncurses5-dev, libneon27, libaprutil1-dev, libtool
	- openjdk-6-jre, openjdk-6-jre-headless, libgtest-dev, screen
	- Lua-5.1 - Berkely DB 5.0 - MySQL Server and Workbench

3. start - Initial setup of development environment

	- Choose editor
	- Setup git user.* config
	- Setup ssh key
	- Register on gerrit
	- Test Gerrit setup
	- Clone repos and checkout a local branch of Core3 origin/unstable
	- Symlinks (idlc)
	- Engine library
	- MySQL database checks
	- Server configuration
	- Tre files
	- build config; run_dev;

4. build - simple build script

	- build always does make -k build
	- build config does 'make config' and 'make clean'
	- build clean does 'make clean'

5. run_dev - Build and run the development server and launch it under gdb on a 'screen'

	***NOTE: run_dev uses gdb in batch mode and starts with the commands
	in ~/run/run_gdb which you can change to your pleasing;
	(breakpoints, dumps, settings etc.)

**************************************************************************************
# The following scripts are also useful...

ack - Nice source grep tool (try: cd ~/workspace/MMOCoreORB/src; ack PlanetManager)

myip -  display the ip of the VM and login port for quick configuration of the windows client

updateip - Get ip address of local eth0 and update galaxy table as needed

latest - do a quick git-stash, git-pull, and git-stash-apply so you can get to the latest code w/o loosing local work

freeze - Save your devenv state so you can repeat the same tests over and over

thaw - allow server to continue from previous state each time you run it

installed - Package and version check sent to /home/*


openfile {filename} - open file in eclipse *FIXME*

eclipse - install eclipse, import project and set git properties. *FIXME*
	(Requires Egit-properties.tar.gz in /home/setup/
*******************************************************************************************
-------
Dropbox 
-------
Option A. Installing Dropbox from source

* TODO Fix this and place in 'options' script *
Download the latest installer package from https://linux.dropbox.com/packages/
Extract the tarball like so:
tar xjf ./nautilus-dropbox-1.6.1.tar.bz2
In most distributions, the following commands should do the rest:
cd ./nautilus-dropbox-1.6.1; ./configure; make; make install;

Option B. Dropbox Headless Install via command line

To install, run the following command in your Linux terminal.
cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -
To start deamon in terminal
~/.dropbox-dist/dropboxd

**************************************************************************************
===============
# Eclipse- Not complete
http://eclipse.org/downloads/
---------------
*Install Eclipse*

	Base install - CDT required
	http://eclipse.org/downloads/packages/release/Kepler/SR2.
	Place tarball in /home/setup/ for 'ide' script. Edit ide script file name as needed

**************************************************************************************
---------------
***How to Upgrade Eclipse on the Development VM***

	***Thanks Valkyra***

Close Eclipse. Download http://www.eclipse.org/downloads/dow...PACKAGENAME.tar.gz to ~/Downloads

Start a console session and type the below commands one after each other;

	cd Downloads
	tar -xvf eclipse-cpp-PACKAGENAME.tar.gz
	mv ../eclipse ../eclipse-old
	mv ./eclipse ../eclipse

Now open eclipse again as normal and select workspace will come up, just choose 'OK'

Right click on the Project MMOCorb-Testing and select 'properties'
Add the c++ include paths as shown in the linked image

http://i.imgur.com/N4rq7jb.png

Then add the pre-processor macro as shown in

http://i.imgur.com/k2CMtHM.jpg

Click OK and then Apply

Once added, select the project again and right click, then index/rebuild (may take a while)

Close Eclipse and then re-open it, Carry on working as normal but with the newer version

