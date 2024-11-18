Common Concepts
###############

General description (non-normative)
===================================

This section is non-normative.
It should help to understand the generic idea of this layered standard.

In order to establish trust in the authenticity of the FMU, all files in the zipped FMU archive need to be genuine.
To establish trust in the authenticity of the files, all files are hashed using a cryptographic hash functions.
The hashes are stored in a mapping from the file name to the corresponding hash.
Using the hash table, the importer can check the individual files for unintended modifications.

Additionally, the hash mapping can be hashed itself.
The overall hash can then be signed cryptographically.
By this, any change in the hashes (and the overall hash) can be cryptographically detected.
Additionally, the cryptographic signature can be used to only validate these FMUs that are to be trusted.

X509 certificates
-----------------

One option to create a trust anchor is to use x509 certificates [IEC9594]_.
These types of certificates are commonly used in current internet communication:
both HTTPS and mail transport encryption (IMAPS/SMPTS) use x509 certificates to authenticate the endpoints.

Such a certificate can be used to distribute a public key that can be used to validate a signature.
The signature is generated using a private key which is a preliminary for the certificate creation process.

With the existing solutions there are also methods established to revoke certificates.
This is required if a private key got compromised and must no longer be trusted.
Typically, such certificate revocation lists (CRLs) are published at a certain location and must be checked by the clients.

One important point is that the certificates are organized in some tree-like structure:
Each certificate is signed by its issuing certificate.
That way, by trusting a certain (root) certificate, that must be crafted and handled in a special way, each child certificate can establish trust indirectly.
As a result, this can reduce the overhead to manage the trust in the various certificates:
once a certain certificate is trusted, all children can as well be trusted.
This imposes both benefits and drawbacks.

* Reduction of overhead simplifies management and especially big companies with many partners might benefit from the structured way.
* As trust is passed on, each intermediate certificate signification entity has a certain responsibility and must obey restriction policies.
  These policies must be carefully defined and build such that no security issues might occur.

Direct exchange of GPG-like keys
--------------------------------

In contrast to x509 certificates, there exists the option to exchange public keys directly.
As a result, each participant needs to be in direct interaction with the corresponding partners.
This imposes a higher management impact than when using x509 certificates.

The benefit of this direct approach is that each company/entity can decide which partners to trust.
Also, the creation of keys is much simpler than creation of a complete public key infrastructure with x509 certificates.
No central signature instance or service is needed.
Instead, a so-called web of trust is formed by the combination of the individual entities which is completely decentralized.

This web of trust allows generally to provide revocation lists as well.
These can be either part of the keys themselves and point to a publicly reachable (but decentralized) web server that publishes revocation lists.
Alternatively, there are currently central exchange servers available for public keys that also allow publishing revocation lists.

.. note:: T.B.D.

Storing of cryptographic information
=====================================

In accordance with the :ref:`introduction on the cryptographic chain file <crypto-file>`, the chain file ``crypto.xml`` must hold all data to establish trust in the FMU.

The XML file must have the root XML tag ``fmu-signature``.
This tag must have one attribute ``version`` which must be a string interpreted as semantic version.
Only version ``1.0`` must be accepted by the importer.
Of the version is higher, the importer should issue a warning to the user that the software is outdated and the FMU cannot be verified correctly.

The ``fmu-signature`` tag must have the tags ``individual-hashes``, ``total-hash``, and ``signatures`` each exactly once.

- The content of the ``individual-hashes`` tag will be described in the section :ref:`hashing`.
- The ``total-hash`` tag must have an empty content but an attribute ``hash``.
  The attribute value is described in :ref:`total-hash`.
- The content of the ``signatures`` tag is described in section :ref:`signatures`.

.. note:: Example of a ``crypt.xml`` file structure

    .. code-block:: xml

        <?xml version="1.0" encoding="UTF-8"?>
        <fmu-signatue version="1.0">
            <individual-hashes>...</individual-hashes>
            <total-hash hash="..." />
            <signatures>...</signatures>
        </fmu-signature>

.. note:: XSD sollte erstellt werden
