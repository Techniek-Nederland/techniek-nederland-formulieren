.. FGO documentation master file, created by
   sphinx-quickstart on Tue Jul  6 21:12:42 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

*******************************************
Practical guide to Techniek Nederland Forms
*******************************************

Dutch objects (like buildings), addresses, installations, products are administrated quite well in different
systems. For instance in the `Kadasters' Basisregistratie Adressen en Gebouwen (BAG) <https://www.kadaster.nl/zakelijk/registraties/basisregistraties/bag>`_
that registers buildings and addresses and the `2BA Technical Product Database <https://2ba.nl/>`_ that registers pretty
much every product used in the Technology Industry in The Netherlands.

One of the strengths of these systems is the low coupling, making it easy to evolve on their own while
still exposing the data to other systems using well-defined API's.

`Techniek Nederland <https://www.technieknederland.nl/>`_ is the employers' organization for the installation sector
and the technical retail sector has started a concept providing all sorts of forms in digital structured
data. This will facilitate software-developers to quickly (automatically) implement the forms provided by
Techniek Nederland, instead of recreating forms manually based on PDF-versions.

Providing the forms in a uniform way is the first step in achieving these goals:

* Efficient and quick adoption of the latest (inspection) forms throughout the sector
* Pre-fill forms based on existing information (re-use)
* Setting up a register for products installed in buildings
* Setting up a register for signing off on (mandatory) inspections on installations

This guide is a tutorial for implementing these forms in a simple way. The scope is limited to requesting the
forms and request some (pre-filled) information to enter on the forms. For more information on the
digitisation initiatives in the sector,
please visit https://technieknederland.nl, https://digigo.nu and of course https://fgoplus.nl.

The guide is split up into three sections. The first covers the architecture and models descriptions. The second
is about the Form structures and technology. The third is the actual tuturial with examples how to fetch the forms.

.. toctree::
   architecture
   forms
   naming-conventions
   tutorials/index



Indices and tables
==================

.. * :ref:`genindex`
* :ref:`search`
