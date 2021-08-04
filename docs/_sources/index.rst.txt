.. Camera Hub documentation master file, created by
   sphinx-quickstart on Fri Jul 23 12:42:55 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Camera Hub's documentation!
======================================

If we want to stitch the images together it's nearly impossible unless the 
camera has some timestamping methods using something like a PTR because 
USB cameras are really hard to synchronize due to its nature of jittering.

If we don't need to stitch the images then we can get the images from the camera and send
them to the backend machine directly. In that case we won't be able to find the exact
position of the defect.

Camera: Grasshopper3 USB3
-------------------------

The datasheet (5.3) says,
"All images pass through the frame buffer mechanism.
This introduces relatively little delay in the system."

Why Grasshopper?

Factors to Consider When Designing a Multiple Camera Array
----------------------------------------------------------
https://www.flir.eu/support-center/iis/machine-vision/application-note/factors-to-consider-when-designing-a-multiple-camera-array/

if the first camera in a line of multiple daisy-chained cameras fails, then all subsequent connected cameras will fail too. 

Limitations
^^^^^^^^^^^

Bus interface:
IEEE1394a – 400Mb/s
IEEE1394b – 800Mb/s
The IEEE1394 specification limits the maximum number of devices on a single bus to 64
Hubs:
- the total amount of data that can be transferred is still limited by the IEEE1394 bus.


Host Adapters:
The number of cameras that can be used to stream images continuously is limited by the IEEE1394 chipset used. 

The LSI (Agere) chipset used in the Point Grey PCI Express card is able to support 8 simultaneous DMA contexts. 
This means that 8 cameras are able to stream at any given time, with a combined total bandwidth of 800Mb/s. 
TI chipsets are able to support 4 simultaneous DMA contexts.

Configuring Synchronized Capture with Multiple Cameras
------------------------------------------------------
https://www.flir.eu/support-center/iis/machine-vision/application-note/configuring-synchronized-capture-with-multiple-cameras/

definition of "the same time" is that the cameras must take start exposing each set of images within microseconds of each other. 
1. use one "primary" camera to trigger one or more "secondary" cameras, using the primary camera's strobe
frame rates of the secondary cameras follow that of the primary camera. 

There are two steps to configuring synchronized capture:

    a) Create a physical connection between the cameras by linking their GPIO pins.
    b) Configure inputs and outputs for each camera either with the SDK demo application or with code.


2. have all cameras triggered by an external hardware trigger (for example, a function generator). Any hardware trigger that provides a 3.3 or 5 V square wave TTL signal can trigger the cameras.


# Exsisting Solutions

USB 3.1 Host Controller Card (35k LKR)
https://www.flir.eu/products/usb-3.1-host-controller-card/


Saving Images at High Bandwidth
-------------------------------
https://www.flir.eu/support-center/iis/machine-vision/application-note/saving-images-at-high-bandwidth/

.. toctree::
   :maxdepth: 2
   :caption: Contents:



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
