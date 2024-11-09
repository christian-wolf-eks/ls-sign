.. _storage-path:

Layered Standard Storage
########################

[*The layered standard requires a fixed folder in the* ``extra`` *directory in the FMU file.*]
The *fmi-ls-crypt* layered standard must use the folder ``extra/de.eks-intec.fmi-ls-crypt``.

Layered Standard Manifest
=========================

The manifest file signals to the importer that the FMU supports this layered standard.
The importer must try to verify the signature as described in this standard.
If the FMU could not be verified, the importr should provide a error message to the user.
Depending on the configuration, the importert must refuse to call or load any library code inside the FMU.

As with any layered standard, a layered standard manifest file ``fmi-ls-manifest.xml`` is required.

.. list-table::
    :header-rows: 1

    -   - Attribute
        - Namespace
        - Value
        - Description
    -   - ``fmi-ls-name``
        - http://fmi-standard.org/fmi-ls-manifest
        - de.eks-intec.fmi-ls-crypt
        - Name of the layered standard in rev. domain notation
    -   - ``fmi-ls-version``
        - http://fmi-standard.org/fmi-ls-manifest
        - 1.0.0
        - Version of the layered standard, using `semantic versioning < https://semver.org/spec/v2.0.0.html>`
    -   - ``fmi-ls-description``
        - http://fmi-standard.org/fmi-ls-manifest
        - Layered standard for handling cryptogrphic trust in FMUs
        - String with a brief description of the layered standard, can be shown to users

.. note:: Example of a layered standard manifest

    .. code-block:: xml

        <?xml version="1.0" encoding="UTF-8"?>
        <fmiLayeredStandardManifest
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:fmi-ls="http://fmi-standard.org/fmi-ls-manifest"
            fmi-ls:fmi-ls-name="de.eks-intec.fmi-ls-crypt"
            fmi-ls:fmi-ls-version="1.0.0"
            fmi-ls:fmi-ls-description="Layered standard for handling cryptographic trust in FMUs"/>

.. _crypto-file:

Cryptographic chain file
========================

The cryptographic chain file must be located in the layered standard path as described in :ref:`this section <storage-path>`.
The file must be called ``crypto.xml``.
The detailled structure is described in the next chapters.
