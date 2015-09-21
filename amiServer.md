# Intro #
# Getting the Sources #
> you can check out the complete source-tree here:
```
 hg clone https://amiserver.openami.googlecode.com/hg/ [local path to write]
```
# Dependencies #

  * Python
  * Mercurial
  * Cherrypy
  * Xmppony
  * Httplib2
  * Simplejson
  * Supay
  * Python-openssl
  * Python setup-tools

> See the Installation Documentation for additional information.

# Developing with Eclipse #
  1. Install the Eclipse IDE
> > http://www.eclipse.org/downloads/
  1. Install Pydev via Direct Download or use the Eclipse update manager
> > http://pydev.org/download.html
  1. Install MercurialEclipseTeamPlugin with the Eclipse update manager
> > http://cbes.javaforge.com/update
  1. Checkout the openAMI Server
    * File => New => Other => Mercurial => Clone Repository using Mercurial
    * URL: https://amiserver.openami.googlecode.com/hg/
  1. Open amiServer.py
  1. Project => Properties
    * Run/Debug Settings => New => Python Run
    * Choose "Run/Debug Settings" and create an new one
    * Choose "Python Run"
    * Give a "Name"
    * Choose the “Project”
    * Choose the "Main Module" (amiServer.py).
    * Go to the Arguments Page:
      * Type in "Program arguments": proc
      * Choose the "Working directory" by clicking "Other" and "Workspace...". Select the “src” folder.
  1. Copy server.properties.default to server.properties

# Installation #

## OpenWRT ##

  1. Connect to Router with Terminal or Putty
```
  ssh 192.168.1.1 -l root 
```
  1. Setup USB Boot
> > Follow Instructions [here](http://nuwiki.openwrt.org/oldwiki/UsbStorageHowto#boot.configuration.kamikaze). And then:
```
  df -h (check active fs)
  /etc/init.d/pivotroot
```
  1. Install dependencies
```
  opkg update
  opkg install python mercurial cherrypy xmppony httplib2 simplejson python-openssl
```
  1. Because mercurial installs itself to /usr/lib/python2.4/site-packages/mercurial so creating a symlink resolves the problem
```
 ln -s /usr/lib/python2.4/site-packages/mercurial /usr/lib/python2.5/site-packages/mercurial
```
  1. Install setup tools:
```
 wget http://pypi.python.org/pypi/setuptoolscurrent
 ash setuptools-0.6c11-py2.5.egg
```
  1. checkout the amiServer
```
 mkdir /workspace
 cd /workspace
 hg clone https://amiserver.openami.googlecode.com/hg/ [local path to write]
 cd /workspace/openami-server
```
  1. copy default properties
```
 cp server.properties.default server.properties
```
  1. Start openAMI with console
```
 python amiServer.py proc
```
  1. Start openAMI without console (in background)
```
 python amiServer.py start
```
  1. Web Frontend is on Port 8080


## Ubuntu ##
  1. Install dependencies
```
 sudo easy_install xmppony cherrypy supay
 sudo apt-get install mercurial python-setuptools 
```
  1. checkout the openAMI Server
```
 hg clone https://amiserver.openami.googlecode.com/hg/ [local path to write]
```
  1. copy default properties
```
 cp server.properties.default server.properties
```
  1. Start openAMI with console
```
 python amiServer.py proc
```
  1. Start openAMI without console (in background)
```
 python amiServer.py start
```
  1. Web Frontend is on Port 8080


# Config #
## /server.properties ##
```
# this is the main config-file 

# if logging is enables, this will be the logfile.
[DataCollector]
file = logs/datacollector.log

# The scheduler features a cron-like format for executing periodical tasks
# TODO: format, sample
[Scheduler]

# The FeedReader currently supports podcast-feeds only. 
# For each episode, there will be an entry in the tree-view
[FeedReader]
mondayjazz = http://www.mondayjazz.com/mj.xml

# Support for virtual file-systems
[Filesystem]
interfaces = PlugInsSupport/interfaces
html = PlugInsSupport/web
properties = server.properties
log = logs

# References to other amiServer instances 
[Global]
lab = 192.168.1.1/ami.wrtv2@aminet.org
dev-box = localhost/ami.lab@aminet.org
kitchen = 192.168.1.170/ami.wrtv1@aminet.org

# amiServer properties
# web  = on/off - Webinterface
# logging = on/off - DataCollector
# TODO
[server]
web = on
logging = off
information = Root Container
interfacerev = PLEASE_DEFINE_THIS
token = ami.lab@aminet.org
master = PLEASE_DEFINE_THIS
architecture = macos
caching = PLEASE_DEFINE_THIS
jabber = off

# TODO
[iTunes]
scriptpath = /Users/markus/fast/tunes.sh

# This defines how the tree-view entries in /Defaults are mapped. 
[Defaults]
playlist = /Audio/LastFM/Playlist
love = /Audio/LastFM/Love
state = /Audio/LastFM/State
coverart = /Audio/LastFM/CoverArt
notification = /Notification/Notification/Prowl
audioback = none
setvol = /System/Openwrt/SetVol
audiopause = /Audio/LastFM/Pause
coverartimg_plain = /Audio/LastFM/CoverArtImage
nowplaying = /Audio/LastFM/Now_Playing
neighbours = /Audio/LastFM/Neighbours
audioskip = /Audio/LastFM/Skip
audioplay = /Audio/LastFM/Library
ban = /Audio/LastFM/Ban
backend = LastFM
library = /Audio/LastFM/Library
audiostop = /Audio/LastFM/Stop

# Path to the PlugInsFolder
[Plugins]
pluginsfolder = PlugInsFolder

# Properties for interfacing Shell-FM
# host = machine shell-fm is running on
# port = shell-fm port
# user = Last.FM username
[LastFM]
host = 192.168.1.1
user = ka010
port = 54311

# Properties for interfacing Shell-FM
# host = machine boxee is running on
# port = boxee port
# user = Last.FM username
[Boxee]
host = 127.0.0.1
user = ka010
port = 8800

[Sensors]
light_lab = /System/Scripts/ShellScript?string=cat /dev/avrBridge0/pins/adc0

[avrBridge]
lib = /PlugInsSupport/libavrBridgeC.so

# Deprecated
[jabber]
jid = ami.lab@aminet.org
pwd = lab
host = ami
groupchat = ami
ressource = lab
groupserver = conference.jabber.org
port = 5222

[AlarmClock]
monday = PLEASE_DEFINE_THIS
tuesday = PLEASE_DEFINE_THIS
friday = PLEASE_DEFINE_THIS
wednesday = PLEASE_DEFINE_THIS
thursday = PLEASE_DEFINE_THIS
sunday = PLEASE_DEFINE_THIS
time = PLEASE_DEFINE_THIS
active = PLEASE_DEFINE_THIS
saturday = PLEASE_DEFINE_THIS


```


## /properties/dashboard.properties ##
```
# The Dashboard is generated entirely from this config file. 
# [Sections] define Dashboard-entries.
# type = std/optionselect - defines the ui element
# title = Title - defines the entries title
# icon = /icon.png - defines an icon for the entry

[TemperaturLivingRoom]
type=std
cam=
title=Temperature
icon=/Filesystem/interfaces/dashboardicons/leaf.png
largetext=35&ordm;C
smalltext=none
link=

[NowPlaying]
type=std
cam=
title=NowPlaying
icon=/Defaults/coverartimg
largetext=/Defaults/getBackend
smalltext=/Defaults/nowplaying
link=/ami.lab@aminet.org/Filesystem/interfaces/Player.interface

[Scenarios]
type=optionselect
icon=/Filesystem/interfaces/dashboardicons/leaf.png
cam=False
title=Scenario
link=/ami.lab@aminet.org/Filesystem/interfaces/LabCam.interface
options = 4
option0 = default
option1 = Security
option2 = Chillout
option3 = Party
cmd = /Defaults/setScenario

[SecurityCamLab]
type=std
icon=http://localhost/ka010/labcam.jpg
cam=True
title=Last Activity
largetext=Lab Cam
smalltext=/Scenarios/Security/LastMotion
link=/ami.lab@aminet.org/Filesystem/interfaces/LabCam.interface
```
## /properties/profiles.properties ##