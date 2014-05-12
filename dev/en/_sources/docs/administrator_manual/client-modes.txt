Physical client mode
********************
Physical client mode is preferred way of launching |GL| client, because it provides best performance. It will run |GL| client session on client machine instead of original operating system installed (if any) on hard drive. Original operating system will stay untouched and will be ready to run again after |GL| client is shut down.

To run physical client steps below:

* connect host machine (|GL| server) and client machines via gigabit switch and cable (CAT 5e or higher)

* on client machines enable LAN PXE boot in BIOS. Often you can find this option under *Network Boot* or *Boot Services*. On newer computers you have to enable *Legacy Mode*.

* boot client machines from LAN. On most computers you can launch LAN boot by pressing F12 key at start.


Virtual client mode
*******************
Virtual client mode is useful users wants to keep working in their favorite operating system (for example your favourite Windows 7 OS) and still want to use GIS.lab. VirtualBox client is provided for Windows, Linux or Mac OSX operating systems.

Installation
------------
* download and install VirtualBox on client system from https://www.virtualbox.org/wiki/Downloads .

* create new virtual machine in VirtualBox (:menuselection:`Machine > New`) with following configuration:

.. figure:: /static/administrator_manual/client-modes/vb-client-new.png
   :align: center

   Creating new VirtualBox machine

* do not create any virtual hard drive

.. figure:: /static/administrator_manual/client-modes/vb-client-hard-drive.png
   :align: center

   VirtualBox hard drive configuration

* configure boot order to boot only from network and enable IO APIC (:menuselection:`Settings > System`)

.. figure:: /static/administrator_manual/client-modes/vb-client-system.png
   :align: center

   VirtualBox machine system configuration

* configure network adapter in bridged mode, make sure you select the PCnet-FAST III (Am79C973) as the adaptor type and allow promiscuous mode for all (:menuselection:`Settings > Network`)

.. figure:: /static/administrator_manual/client-modes/vb-client-system-network.png
   :align: center
   
   VirtualBox machine network configuration

* enjoy

.. figure:: /static/administrator_manual/client-modes/gislab-vb-client-qgis.jpg
   :align: center

   Running GIS.lab virtual client on Windows

Additional configuration
------------------------
To set custom client display resolution run following command on host machine:: 

   $ VBoxManage controlvm "GIS.lab client" setvideomodehint <xresolution> <yresolution> 32

for example:: 

   $ VBoxManage controlvm "GIS.lab client" setvideomodehint 1000 660 32

