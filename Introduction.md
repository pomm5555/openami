# openAMI #

# Introduction #


The openAMI project aims to become a flexible and highly customizable ambient intelligence and home automation solution built completely using free software, off the shelf hardware and DIY electronics.

Our final goal is to provide two different frameworks:

## Home Automation ##

A framework providing execution and communication- as well as physical infrastructure in a smarthome environment.

### Hardware Components ###

#### Infrastructure ####
> In order to keep the overall costs (hardware and power-consumption) at a minimum we use
> off-the shelf wifi-routers running openWRT (a embedded linux) to provide
> wireless infrastructure as well as entertainment features like audio streaming in separate
> rooms.

#### I/O ####
> For interfacing sensors and actors in the real world, we have developed a small, easy to
> build microcontroller board that connects via USB and can be attached to any PC, Laptop,
> Server or openWRT based embedded device.

### Software Components ###
#### amiServer ####
> On the software side we have a central daemon that handles communication, events and
> execution.It is written completely in python and currently known as "the amiServer"
> Infrastructure

> The amiServer implements the following two main components in order to provide the
> necessary infrastructure:

  * Communication-Engine

  * Execution-Engine

#### User Interface ####

> We aim to provide a set of three different User Interfaces designed specifically for the
> following use-cases:

  * Mobile
> > For controlling the system from a smartphone, we provide a customizable javascript-based webinterface. Now there is an Anroid App called ECOntol with a lot new Features. Read the ECOntrol page for more information.


  * Desktop
> > To offer quick access from Desktop Systems or Laptops, there will be a Mac OSX
> > Dashboard Designer to generate custom controller or monitor widgets.

  * HTPC
> > Of course, Mediacenter integration is a must, we plan to accomplish this by providing
> > a set of plugins for the popular open source Mediacenter XMBC.

#### Plugins ####


> In order to make the system easily extendable, the amiServer offers a Plugin Interface.

## Ambient Intelligence ##

//TODO