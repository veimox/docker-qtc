*************************************
Docker images for QtCreator ROS CI/CD
*************************************
The objective of this image is to do *as much as possible* to ease the compilation process of the project `ros_qtc_plugin`_. More information about this repo can be found in the link, but basically provides useful tools to work with `ROS`_ C++ packages.

As of today QtCreator does not have a -lets say- *friendly* way of adding plugins which can be done in three ways:
  
1. You get QtCreator people to compile and deploy the plugin them selves. This leads to a lost of lifecycle control from the plugin developer side.
2. You compile the plugin for every single QtCreator version that your end users might have and let them download and install the plugin manually. This could be automated but it would require to support many, many edge cases.
3. You compile the full QtCreator along with the plugin and deploy that as a single unit that can be installed along with any other QtCreator version. This is sort of invasive, but more scalable.      
     
This plugin has decided to opt for option number 3, compile the full thingy. One of the disadvantages of this method is that we have to... compile QtCreator itself to later on compile the plugin. It takes **a lot** of time to compile the full project and if that is done in the main project it would destroy the early feedback purpose of CI. Thus, this repo does everything needed to ease the path of the plugin compilation.

Flow
====
There are two OS supported: 

1. Ubuntu 16.04: xenial
2. Uubntu 18.04: bionic
     
And there are actually three things being compiled: 

1. QtCreator
2. QTermWidget
3. Yaml CPP
     
The last two libraries are needed for additional features of the plugin.

For each OS and plugin the process it such the repos will be cloned, compiled and placed in an specific folder structure.

Dependencies
============
This Docker image relays on another Docker image called `docker-qt`_, where Qt itself and specific plugins are compiled at the desired version. That project create images such:

* qt:xenial-5.12.4
* qt:bionic-5.9.8 

So QtCreator can be compiled against different Qt versions.

.. _docker-qt: https://github.com/veimox/docker-qt

.. _ROS: http://ros.org

.. _ros_qtc_plugin: https://github.com/ros-industrial/ros_qtc_plugin