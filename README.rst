GIS.lab user manuals.

Building manuals
----------------
Website is a static generated website using Sphinx (http://sphinx-doc.org/), 
based on restructured text sources (rst: http://docutils.sourceforge.net/rst.html)
and html (jinja2) templates.

Most sources are in source/site. Only frontpage and landingpages are in theme/qgis-theme


Sphinx project is based on QGIS Documentaion Project. Thanks !
Styling is in theme/qgis-theme.

Building is only tested on Linux systems using make.


Build Tools
-----------
To be able to run localisation targets you will need Sphinx 1.2b3 which comes with pip. 
Sphinx coming with most distro's is just 1.1.3. You will get an gettext error with those.

Best to run the make file in a virtual env ( http://www.virtualenv.org/ ):

Move to a directory (~/myvirtualenvs/) and create a virtualenv enabled dir:

    virtualenv sphinx  # one time action, only to create the environment
    cd sphinx

And activate this virtualenv

    source bin/activate 
    # now you will see sphinx before your prompt:
    (sphinx)richard@mymachine

Now always activate your environment before building. To deactivate, you can do:

    deactivate

If your linux is package based and doesn't have current versions of
the tools, it is best to install them in the virtual env too.

You can install all tools in one go via the REQUIREMENTS.txt here in the root of this repo:

    pip install -r REQUIREMENTS.txt

Alternatively do it one by one:

    pip install sphinx==1.2b3

    pip install sphinx-intl

Then build:

    make html (to build the english language)

