Architecture & Models
======================

This section explains the eco-system for which this Forms API is designed, followed by a definition of
all entities available. Terms will be specified in both English and Dutch.

.. contents:: Table of Contents
   :depth: 2
   :local:
   :backlinks: none

Architecture
------------
Forms are a means for an Installer to describe a situation and produce a Report that is in turn being required by
some sort of Regulations. Regulations can be anything from actual law to in private defined certifications. Belows
image explains what pieces of information are available in the field and how flow from the actual Form to the
Report to the Regulations. Each entity (piece) is explained below.

.. image:: _static/images/fluxility-techniek-nederland-forms-architecture.png
   :alt: System architecture

Entity definitions
-------------------

Form (formulier / protocol /checklist)
######################################
The main entity will be the `Form` (Protocol, checklist etc). A set of questions regarding the current state of
a system installed in an object (eg. building). These forms are defined by experts or expert groups and are provided
by for instance `Techniek Nederland <https://www.technieknederland.nl>`_ or `ISSO <https://isso.nl>`_. Forms should
be designed in such a way that it will never ask question that do not lead to data ending up in the report.

Report (inspectierapport / rapportage)
######################################
The `Report` is a (finalized) document holding information that was provided using the filled out `Form` in combination
with conclusion drawn upon the provided data. The Reports content must comply to rules as stated by the regulations.

Regulations (BRL, NTR, NTA, NEN, ISO)
######################################
Most of these forms are created with regulations in mind, or even created
to fully comply with these regulations. Regulations can be governed by certifying instance, government etc.

Installation company (Installatiebedrijf)
##########################################
A company responsible for the installation of an (technical) product inside an Object (building). In order to do
most inspection, companies need to be certified.

Object (Building, Gebouw, Bouwwerk, Pand, Werkadres)
#####################################################
Most of the times an Object will be a building, but it could also be for instance a meadow (solar panels).
Objects in the Netherlands are registered by the Kadaster and kept in a database called BAG.
Each Object (and subobject) is document with a unique BAG ID. See
https://www.kadaster.nl/zakelijk/producten/adressen-en-gebouwen/bag-api-individuele-bevragingen.

Client (Opdrachtgever)
#######################
The Client is the person or company who commissioned the inspection. Most often this will be the owner or responsible
person toward the given installation.

.. note::
    In the near future this definition needs to be improved, because their
    are many roles of responsibility towards an installations. For instance the owner of the building, the owner
    of the installation, the user of the installation etc.

Installation (System, Installatie, Systeem)
###########################################
An Installation is a Product that is installed and serving it's purpose in or on an Object.

Installation Parts (Installatie-onderdeel, Sub-systeem)
#######################################################
Installations for a hierarchy (tree), where each Installation might consist of sub-installations. For instance

* Central Heating System consist
    * Heat generator
        * burner
        * expansion vessel
    * Radiator
    * Gas transport towards generator
    * Water transport to radiators

An inspection might be about just the Heat Generator and it's parts (burner and expansion vessel). Another might
be about the full heating system, or just on the Gas transport.

Product data (stored in 2BA)
#######################################################
Actual information on products (non-installed) can be found in the `2BA Product database <https://2ba.nl/>`_.
It holds a rich set of products with all their features described (in `ETIM <https://www.etim-international.com/>`_),
making it easy to uniformly enter information on the installation
that is being inspected. The product information is provided to 2BA by the manufactures themselves
and therefore quite accurate. This data can be used to prefill forms when describing the installed product.

Current State
##############
The whole reason for filling out the form will be the Current State of the Installation. This covers anything from
'having a new Installation installed' to 'a leakage' to 'actual power consumption compared to factory standards' and
of course the amount CO and CO2 being produced by the installation.

Classification systems
--------------------------------------

NL/SFB
#######

There is a Dutch classification standard for describing types of installations and product. It's a determination to
with each level becoming more specific. Level one is 'heating', 'cooling' etc, level two can be 'central', 'local' etc,
and the deepest can be type of fuel used. See https://ketenstandaard.nl/standaard/nl-sfb/.

ETIM
####

A second standared for product classification is ETIM. Where NL/SFB is focussed mainly on creating groups of products,
ETIM also aims at defining all properties of products in a standardised way. See https://www.etim-international.com/.

Naming standards and conventions
---------------------------------
A first attempt has been made to produce a list of standard terms to use throughout the forms. There are many
ways to name something (eg. 'Naam', 'Voornaam + Achternaam', 'Volledige naam'). The draft version of this
document can be downloaded
`Form Fields Naming Convensions (XLSX) <_static/files/techniek-nederland-forms-naming-convention.xlsx>`_. This
document is currently maintained by `Peter Zwakhals @ Techniek Nederland <mailto:p.zwakhals@TechniekNederland.nl>`_.
