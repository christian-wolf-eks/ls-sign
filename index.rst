.. Test Project documentation master file, created by
   sphinx-quickstart on Thu Nov  7 17:42:26 2024.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Test Project documentation
==========================

.. Add your content using ``reStructuredText`` syntax. See the `reStructuredText <https://www.sphinx-doc.org/en/master/usage/restructuredtext/index.html>`_ documentation for details.

Based on the `FMI 2.0.2 standard <https://fmi-standard.org>`_, this layered standard defines a way to sign FMUs cryptographically.
That way, the users of FMUs can create trust in the simulation models implemented and their authenticity.


Copyright © 2024 Christian Wolf.

This document is licensed under the Attribution-ShareAlike 4.0 International license.
The code is released under the 2-Clause BSD License.
The licenses text can be found in the LICENSE.txt file that accompanies this distribution.


.. toctree::
   :maxdepth: 2
   :caption: Contents:

   content/introduction.rst
   content/manifest.rst
   content/concepts.rst
   content/individual-files.rst
   content/crypto.rst
   content/appendix.rst


.. rubric:: References

.. [IEC9594] ISO/IEC 9594-8, https://www.iso.org/cms/render/live/en/sites/isoorg/contents/data/standard/08/03/80325.html

.. [Coreutils] GNU Coreutils, https://www.gnu.org/software/coreutils/

.. [RFC4648] RFC4648, The Base16, Base32, and Base64 Data Encodings, https://datatracker.ietf.org/doc/html/rfc4648
