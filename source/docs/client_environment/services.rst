Services
********

Files storage and sharing
=========================

Home directory for personal data storage is created for each |GL| user. Additionally, structure of shared directories (each with different purpose and permissions) is available.

.. figure:: /static/client_environment/client-home-files.png
   :align: center

   |GL| client home files


Personal files storage
----------------------

User's home directory is pre-populated with following directories dedicated for personal data storage:

 * **Tmp** - storage of temporary or test files. This directory is excluded from backup (do not keep important files here)
 * **Downloads** - storage of downloaded files. Many applications like Firefox are automatically using this directory for downloads. This directory is also excluded from backup (move important downloads elsewhere from here)
 * **Documents** - storage for office documents
 * **Music** - storage for music files. Music applications automatically search here
 * **Pictures** - storage for pictures and photos. Picture and photo applications automatically search here
 * **Videos** - storage for video files
 * **Projects** - main working directory. This directory is recommend for storing project's data


Files sharing
-------------

Following directories are prepared for different levels of files sharing:

 * **Repository** - data installed by |GL| administrator

   * administrators (members of labadmins group) - read and write permissions
   * all users - read permissions

 * **Share** - directory contains personal shared subdirectories owned by |GL| users. All data and project files for |GLW| must be placed here

   * directory owner - read and write permissions
   * all users - read permissions

 * **Barrel** - free files sharing directory. All users can read and write any files


Chat
====

|GL| comes with simple chat service for interactive messaging within |GL| network. In order to start using chat service, it is required to launch chat client in applications menu :menuselection:`Internet --> Pidgin Internet Messenger` (no additional configuration of access credentials is required). Than, chat client will stay connected until the end of user session.

.. figure:: /static/client_environment/client-chat.png
   :align: center

   |GL| chat


By default, all messages are posted in chat room and are readable for each user. It is possible to start private chat, by choosing user in right pan.

WARNING: all messages, including private messages, are send WITHOUT encryption. Do NOT use chat for sending confidential data without additional encryption.


Shared geodatabase
==================

|GL| provides shared database storage with spatial support for tabular and vector data. Storage for each |GL| user is available in database called **gislab**. Access to this database is preconfigured in all GIS tools provided by |GL|.

By default, each user is allowed to create database objects in his own database schema (think about schemas as directories). User's schema is readable only for it's owner. Manual permissions assignment is required to allow other user's access (:menuselection:`GIS.lab --> Shared Geo Database`).

.. figure:: /static/client_environment/client-database.png
   :align: center

   |GL| database


GIS project creation, data processing and analysis
==================================================

|GL| provides unique, single tool capable to solve most of the ordinary GIS user's needs in one place. It is available via :menuselection:`GIS.lab --> GIS Project and Data Processing`.

.. figure:: /static/client_environment/client-gis-project.png
   :align: center

   GIS project creation, data processing and analysis


**Features**

* **File formats** - AutoCAD DXF, ESRI Shapefile, GeoJSON, GML, GeoJPEG, KML, Microstation DGN v.7, OpenStreetMap XML and PBF, SQLite/SpatiaLite, TIFF/GeoTIFF
* **Geodatabases** - PostgreSQL/PostGIS, MS SQL Spatial, Oracle Spatial
* **Base maps** - OGC WMS services or public on-line maps like OpenStreetMap
* **Advanced vector data editing**
* **Vector and raster data analysis**
* **Print output creation** - output maps can include legends, labels, scalebar, vector shapes and arrows, tables and html content (landscape or portrait) and can be produced in PNG or PDF format

.. note:: *GIS project creation, data processing and analysis* is based on QGIS 2.2. In addition, it contains bug fix updates and some custom features.


GIS project publishing
======================

TODO: will be done after GIS.lab Web plugin will be updated.
