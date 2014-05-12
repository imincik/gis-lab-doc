Quick Start
***********

.. warning:: Server installed to virtual machine contains its own DHCP server. DHCP server access is restricted by MAC addresses when GISLAB_UNKNOWN_MAC_POLICY=deny. Do not change this configuration when you are connecting to your corporate LAN and always consult it with your system administrator.

You are absolutely safe to install with *GISLAB_UNKNOWN_MAC_POLICY=allow* on machine without Ethernet connection to any existing LAN.
Installation will NOT modify anything on your host machine. Every operation is done inside of virtual machine.

All lines beginning with *$* (dollar) character are shell commands which must be run in command window. In most cases you can copy and paste commands from this page, but sometimes you will need to modify them little bit to suite to your conditions.

**On Linux**, open terminal window in :menuselection:`Accessories > Terminal Emulator` menu.

.. figure:: /static/quick_start/installation/terminal-window-linux.png
   :align: center

   Terminal window on Linux

**On Windows**, open Command Prompt window in :menuselection:`Start > Accessories > Command Prompt` or :menuselection:`Start`, type *cmd* and hit **\[Enter\]** menu.

.. note:: You can open Command Prompt in chosen directory via **\[Shift + RightMouseClick\]** on white space and choosing *Open command window here*.

.. figure:: /static/quick_start/installation/cmd_windows.png
   :align: center
   
   Command prompt on Windows

Terminology
-----------
* host machine - main machine where Vagrant, VirtualBox and |GL| package is installed
* |GL| server - |GL| server environment which runs as virtualized system on *host machine*
* client machine - machine which runs |GL| client system launched from |GL| server
* |GL| client - |GL| client environment which runs on *client machine*


Installation on Linux and Windows
=================================

Software requirements
---------------------
* host machine with working Linux, Windows or Mac OSX operating system (in our case Xubuntu 12.04.2 LTS and Windows 7)  
* VirtualBox
* Vagrant 1.5 or higher

Install VirtualBox on Linux
---------------------------
* add VirtualBox repository’s key ::

  $ wget -q http://download.virtualbox.org/virtualbox/debian/oracle_vbox.asc -O- | sudo apt-key add -

* add VirtualBox repository to system ::

  $ sudo sh -c 'echo "deb http://download.virtualbox.org/virtualbox/debian precise contrib" >> /etc/apt/sources.list'

* install Dynamic Kernel Module Support Framework ::

  $ sudo apt-get update && sudo apt-get install dkms

* install VirtualBox ::

  $ sudo apt-get install virtualbox-4.3

Install VirtualBox on Windows
-----------------------------
* download VirtualBox installer from https://www.virtualbox.org/wiki/Downloads (VirtualBox for Windows hosts version)
* install VirtualBox by running the installer wizard using default settings

Install Vagrant on Linux
------------------------
* remove previously downloaded Vagrant packages ::

  $ rm -vf ~/Downloads/vagrant_*.deb

* download Vagrant from http://www.vagrantup.com/downloads.html

* install package ::

  $ sudo dpkg -i ~/Downloads/vagrant_*.deb
  $ sudo apt-get -f install

Install Vagrant on Windows
--------------------------
* download Vagrant from http://www.vagrantup.com/downloads.html (Windows Universal version)
* install Vagrant by running the installer wizard using default settings
* after installation you will be asked to restart your PC

Install Vagrant Box on Linux and Windows
----------------------------------------
* run command to download base operating system image (you can run this command from whatever directory) ::

  $ vagrant box add precise32-canonical http://cloud-images.ubuntu.com/vagrant/precise/current/precise-server-cloudimg-i386-vagrant-disk1.box

.. note:: Enter above command in one line.

Download |GL|
-------------
* download latest |GL| package from https://github.com/imincik/gis-lab/releases/latest
* unpack |GL| package in your working directory

Configure |GL|
--------------
* move to directory where you have extracted |GL| package
* open configuration file *config.cfg* in plain text editor (Leafpad, Mousepad, Gedit on Linux or Notepad, Notepad++ on Windows)
* add client machines MAC addresses to *GISLAB_CLIENTS_ALLOWED* (recommended)

.. figure:: /static/quick_start/installation/config.cfg.png
   :align: center

   File config.cfg

or

set GISLAB_UNKNOWN_MAC_POLICY=allow to allow all MACs (see warning at a top of this page)  

Install |GL| and create user account
------------------------------------
* move to directory where you have extracted |GL| package (you should already be there)
* run installation command :: 

  $ vagrant up

.. figure:: /static/quick_start/installation/vagrant_up.png
   :align: center

   vagrant up command output

.. note:: Installation can take to run from 20 minutes to few hours, depending on your machine and Internet speed. 
   If your machine contains multiple network adapters, you will be asked to choose one. Select one corresponding to your wired network adapter (on Linux it is usually 'eth0')

* create user account *lab* with password *lab* :: 

  $ vagrant ssh -c "sudo gislab-adduser -g User -l GIS.lab -m lab1@gis.lab -p lab lab"


Client machine launch
=====================
It is possible to launch |GL| client in two modes - *Physical client* or *VirtualBox client* mode.  

If you do not changed value of *GISLAB_UNKNOWN_MAC_POLICY* in configuration file *config.cfg* to *allow*, you need to allow MAC address of each client in *GISLAB_CLIENTS_ALLOWED* configuration.  

.. note:: If you do not know MAC addresses of client machines, good way to collect them, is to simply try to boot them from |GL| server and than run following command to get list of denied MAC addresses on server. ::

   $ vagrant ssh -c "sudo grep -e 'DHCPDISCOVER.*no free leases' /var/log/syslog"

Add collected MAC addresses to *GISLAB_CLIENTS_ALLOWED* configuration and do not forget to run ::

   $ vagrant ssh -c "sudo gislab-clients-allowed"

to load them.

After configuring your client machine to boot from LAN you will be able to successfully launch |GL| client session.


|GL| project
============
.. note:: Following steps are created from the perspective of user *lab1*. If you choose to use another user account, replace string *lab1* with your user name in all steps.

* log in to |GL| client machine using *lab1* account with password *lab* and copy example Natural Earth data from *~/Repository* directory to *~/Share/lab* directory

.. figure:: /static/quick_start/gis-project/01_copy_data.png
   :align: center

   Data copying

Create project creation and publishing
--------------------------------------
* launch *GIS Project and Data Processing* application (QGIS) (:menuselection:`GIS.lab > GIS Project and Data Processing`)

.. figure:: /static/quick_start/gis-project/02_gis_project_and_data_processing.png
   :align: center

   GIS Project and Data Processing application (QGIS)

* save empty project as *~Share/lab1/first.qgs* (:menuselection:`Project > Save as`)

.. figure:: /static/quick_start/gis-project/03_save_project_as.png
   :align: center

   Saving project

* add new SpatiaLite layers database connection (:menuselection:`Layer > Add SpatiaLite Layer > New`)

.. figure:: /static/quick_start/gis-project/05_connect_spatialite_layers.png
   :align: center

   Connecting SpatiaLite layers

* browse Natural Earth database file in *~/Share/lab1/natural-earth/natural-earth.sqlite*

.. figure:: /static/quick_start/gis-project/06_browse_spatialite_file.png
   :align: center

   Browsing SpatiaLite database file

* load previously connected Natural Earth layers (:menuselection:`Layer > Add SpatiaLite Layer > Connect`) and select required layers (**\[CTRL + left mouse click\]**)

.. figure:: /static/quick_start/gis-project/07_load_layers.png
   :align: center

   Loading layers

* browse loaded layers in map canvas

.. figure:: /static/quick_start/gis-project/08_browse_layers.png
   :align: center

   Browsing loaded layers

* set project projection to *EPSG:3857* and activate on-the-fly CRS transformation in (:menuselection:`Project > Project Properties > CRS`) and click **\[Apply\]**

.. figure:: /static/quick_start/gis-project/11_project_crs.png
   :align: center

   Setting project projection

* Browse layers in Pseudo Mercator (EPSG:3857)

.. figure:: /static/quick_start/gis-project/12_browse_layers_3857.png
   :align: center

   Browsing layers in Pseudo Mercator

* Set OWS server properties

.. figure:: /static/quick_start/gis-project/14_ows_server_properties.png
   :align: center

   Setting OWS server properties

* Finally save project again (:menuselection:`Project > Save`)

Publish project with |GL| Web
--------------------------------
* publish your project by clicking on |GL| Web icon and pressing **\[Publish\]** button in dialog window

.. figure:: /static/quick_start/gis-project/18_publish_project.png
   :align: center

   Project publishing

* enjoy |GL| Web application.

.. figure:: /static/quick_start/gis-project/19_gislab_web.png
   :align: center

   GIS.lab Web application

Client machine stop
===================
Once you are done with your work, log out from client machine and choose **\[Shut down\]** in :menuselection:`Preferences` menu at login screen to shut down whole |GL| server run command :: 

   $ vagrant halt

which will take server virtual machine to *power off* state.

.. warning:: Make sure that all client machines are off before running halt command.

You will be able to turn server on again by running ::

   $ vagrant up
