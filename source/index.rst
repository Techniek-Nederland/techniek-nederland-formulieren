.. FGO documentation master file, created by
   sphinx-quickstart on Tue Jul  6 21:12:42 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

****************************
Practical guide to FGO Forms
****************************

The Netherlands have created a quite rich data infrastructure to keep track of objects (eg. buildings), installations,
products etc. One of the strengths of these systems is the low coupling, making it easy to evolve on their own while
still exposing data using well-defined API's

This guide is a tutorial for implementing the FGO forms in a simple way. The scope is limited to requesting the
forms and request some (pre-filled) information to enter on the forms. For more information on the total project,
please visit https://technieknederland.nl, https://digigo.nu and of course https://fgoplus.nl.

The guide is split up into three sections. The first covers the architecture and models descriptions. The second
is about the Form structures and technology. The third is the actual tuturial with examples how to fetch the forms.

.. toctree::
   architecture
   forms
   tutorials/index



Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
