# Architecture #


## General ##

The following shows the general system architecture, based on a embedded-linux operating system, there is:

  * the avrBridge for connecting actors and sensors
  * a Python runtime

based on the Python runtime lives the amiServer, which consists of the following subsystems:

  * a Plugin-System for adding functionallity and interfacing external software
  * a Http-Interface remote controlling Plugins
  * a Web-Interface that serves as a User-Interface for the Http-Interface

![http://www.openami.de/wiki/img/arch.png](http://www.openami.de/wiki/img/arch.png)
<br><br>



<h2>Plugin System</h2>

The Plugin System simplifies integration of external software components.<br>
A Plugin may contain User-Interface elements, these are generated automatically in form of a Javascript based Web-Interface.<br>
All Plugins that define User-Interface elements are mapped directly to a Tree-View in the generated Web-Interface, so for each Plugin there is an entry in the Tree-View.<br>
<br>
A lot of Plugins for integrating media-players or other commonly used software components already exist, also with support for different Platforms like openWRT or Mac OSX.<br>
New Plugins however can be realized in Python with only a few lines of code.<br>
<br>
<br>
<img src='http://www.openami.de/wiki/img/plugin-system.png' />
<br><br>



<h2>Plugin</h2>

Each Plugin consists of a Container, its Content.<br>
The Plugin's Content-Container may be represented as a User-Interface element and may contain any number of Child-Containers or subclasses of Container.<br>
<br>
<br>
<img src='http://www.openami.de/wiki/img/plugin.png' />
<br><br>


<h2>HTTP-Interface</h2>

The HTTP-Interface may be compared to a REST-Interface. The Plugin-Tree is mapped directly to URLs, so each Plugin and also each of it's Commands can be identified by a unique URI.<br>
<br>
Additional Parameters can be passed to a Command by using HTTP-GET parameters or by encoding the data in JSON-format.<br>
<br>
<h2>The Residence File</h2>
The Residence data like levels, rooms and the devices with each state is located in the MyEstate.xml. Here you can configure the system to fit your home.