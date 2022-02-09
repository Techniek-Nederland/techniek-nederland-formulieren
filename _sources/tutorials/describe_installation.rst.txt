Describe an installation
------------------------

There will be a lot of forms in the system and browsing them all can be quite cumbersome. For the form (meta) we'll need
to describe the installation anyway, so if we start with defining the installation we can then filter the list of forms
to the relevant ones to this project.

Basic model for an Installation

.. class:: BaseInstallation

    For filling out forms only little information is required on each installation. It can be reduced to
    'where' it's installed, what type (NL/SFB and ETIM) it is and what size (power).

    .. attribute:: building_id

        A reference to the Object/Building in which this system is installed. It's up to you if you choose
        to use a BAG ID or something of your own. In the (near) future it might be relevant to save extra information
        in your database, regarding for instance the year of build for the Object in which the installation has been
        installed. For now, the building is not used for filtering yet.

    .. attribute:: nlsfb_code

        A reference to the group this installation belongs too. For a list of NLSFB code, please see
        https://ketenstandaard.nl/standaard/nl-sfb/. In the near future the NLSFB will be provided through an API
        too.

    .. attribute:: etim_product_class

        The second determination is by `etim_product_class`, also available through https://ketenstandaard.nl/standaard/etim/.
        If you choose to connect with the 2BA Product database, you can easily lookup the ETIM Product Class for every
        installation.

    .. attribute:: children

        A installation might consist of multiple parts. For instance if you're defining a field of solar panels, the
        main installation is the field where the children are the panels.

