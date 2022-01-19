Forms
=====

The goal of FGO forms is to define the forms in such a way, that other (developing) companies can use it to
automatically generate the actual forms. This should allow them to convert it into a new app, a PDF-document or
a new format that can be read by some other system. Essential to this approach, is that the way of storing the
forms should be fully descriptive and structured, in order to have it processed by other systems.

Form structure
--------------------------------------

Each form consists of the two sections. The meta-part and the specific form fields. The meta-part is always the same
and consists of the following elements:

* What Company filled out the form
* Who filled out the form
* Who commissioned filling out the form / owner of installation
* What Installation + What Object (installation implies object)
* What date


The specific forms fields are of course different for every form, though a standard is in the making to formalize
the sections and questions as much as possible.

When requesting a form, the meta field are **not** provided, you can add them yourself.


Form technology
--------------------------------------

The applications makes use of `Schema JSON <https://json-schema.org>`_ for
all definitions of data and also forms. The forms components a defined using
a thin version of the `FormIO <https://github.com/formio/formio.js/wiki/Components-JSON-Schema>`_.
You can choose to implement your own interpreter, mapper or use one of the
open-source solutions provided by `FormIO Github <https://github.com/formio/formio>`_.
Please note that only the form components are used.
