Introduction
############

Versions and changelog
======================

All released versions should be mentioned here and the major updates summarized.

.. list-table::
    :header-rows: 1

    -   - Version
        - Release date
        - Description
    -   - 1.0.0
        - not released yet
        - Initial version

Motivation
==========

FMI was founded to simplify exchange of simulation models.
The exchange of FMUs between companies or entities is in an ideal world a good solution to share knowledge and avoid redundant modelling effort.
In reality the import of a foreign FMU model involves execution of binary code from the FMU.
Depending on the type of transport and the involved security measurements, the user must trust the FMU (or not) and decide to execute the binary code.
Without executing the code, usage of the FMU is impossible.

One might be able to establish transport-based security measurements:
any transport over the internet is encrypted and signed in order to prevent tampering with the payload of the transport.
The problem with this approach, however, is the data at rest is not protected.
Any server on the network route might cache or save the payload (also as part of the process like storing an e-mail).
The data stored on these servers is no longer protected as the transport-oriented protection only protected the actual point-to-point transport.

The solution to making the complete process secure lies in end-to-end security (E2ES).
However, the usage of cryptographic algorithms is not trivial and imposes quite some traps for the non-security-educated user.
Especially the handling of keys and the involved trust is of high importance.
Ideally, this trust can be defined on a policy level such that any company or entity can set their individual policy.

This layered standard should simplify the E2ES and store all relevant data into the actual FMU.
That way, the FMU can be considered a single sealed file.
It can be checked anytime later for tampering or accidental modifications of the file.
As the FMU itself is cryptographically signed, the transport security is no longer mandatory.
Also, the data at rest is protected.
By defining machine-readable structures in the layered standard, the E2ES can be enforced by exporting and importing software.
The complex and error-prone cryptographic processes are thus hidden from the end-user and can be tested well.

.. note::
    T.B.D.

How to read this document
=========================

The standard document is in HTML allowing use of in-document links.

.. By pressing "t", the table of contents can be displayed on the left side or hidden.

In key parts of this document, non-normative examples are used to help understand the standard.

Conventions used in this document:

- Non-normative text is given in square brackets in italic font:
  [Especially examples are defined in this style.]

  .. note::
        Should be finished later on.

- The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in `RFC 2119 <https://tools.ietf.org/html/rfc2119>`_ (regardless of formatting and capitalization).


Rough outline of the approach
=============================

The FMU is first created using the exporter in a classical way.
Before actually bundling the FMU into a zipped archive, the existing files are hashed and cryptographically signed.
The signature is added to the bundle and everything is zipped.

The importer checks the signature and hashes of the embedded files before actually running the FMU.
This ensures that no binary data is executed before trust in the FMU's content is established.

.. note::
    
    T.B.D.

- No binary code execution
- Hashing + signture
