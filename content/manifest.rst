.. _storage-path:

Layered Standard Storage
########################

.. note::
    The layered standard requires a fixed folder in the* ``extra`` *directory in the FMU file.

The *ls-sign* layered standard must use the folder ``extra/de.eks-intec.fmi.ls-sign`` within the zipped FMU bundle.

Layered Standard Manifest
=========================

The manifest file signals to the importer that the FMU supports this layered standard.
The importer must try to verify the signature as described in this standard.
If the FMU could not be verified, the importer should provide a error message to the user.
Depending on the configuration, the importer must refuse to call or load any library code inside the FMU.

As with any layered standard, a layered standard manifest file ``fmi-ls-manifest.xml`` is required.

.. note::
    The existence of the file ``extra/de.eks-intec.fmi.ls-sign/fmi-ls-manifest.xml`` indicates that the FMU adheres to the *ls-sign* layered standard.
    This is defined in the core standard.
    Additionally, some basic information about the layered standard is given in this file.

.. list-table::
    :header-rows: 1

    -   - Attribute
        - Namespace
        - Value
        - Description
    -   - ``fmi-ls-name``
        - http://fmi-standard.org/fmi-ls-manifest
        - de.eks-intec.fmi.ls-sign
        - Name of the layered standard in rev. domain notation
    -   - ``fmi-ls-version``
        - http://fmi-standard.org/fmi-ls-manifest
        - 1.0.0
        - Version of the layered standard, using semantic versioning [SemVer]_
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
            fmi-ls:fmi-ls-name="de.eks-intec.fmi.ls-sign"
            fmi-ls:fmi-ls-version="1.0.0"
            fmi-ls:fmi-ls-description="Layered standard for handling cryptographic trust in FMUs"/>

The importer must check the version of the layered standard.
If a newer major version [#major-part]_ in the manifest is found than the importer knows, the FMU must be rejected as signed invalidly.

.. _crypto-file:

Cryptographic chain file
========================

This layered standard uses the so-called cryptographic chain file to store relevant data.
The file must be called ``crypto.xml`` and located in the layered standard path [#lspath]_.
The detailed structure is described in the next chapters.

.. [#major-part] *The first digit of the semantic version string*

.. [#lspath] *The path of this layered standard is* ``extra/de.eks-intec.fmi.ls-sign``
