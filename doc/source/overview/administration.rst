Project Administration
######################

The PyAnsys project allows you to create your own workflows and 
interfaces to Ansys products using Ansys APIs. While using PyAnsys 
libraries requires that the relevant Ansys products are licensed 
either directly or indirectly, you can distribute your custom-made 
applications and workflows internally or externally.


Licensing and Approval
======================
To allow for commercial use, a PyAnsys library must use the MIT
license. Because this license falls in the BSD-style license class,
PyAnsys libraries can be used as a shared library with no
restrictions. This follows the pattern of including PyAnsys as a
dependency in ``install_requires`` in :ref:`The \`\`setup.py\`\` file`.

Should you choose to copy and include any PyAnsys project source uses,
to make your library suitable for commercial use, you need only a copy
of the original PyAnsys `MIT License`_ in the reused code.

To view this license, see `The \`\`LICENSE\`\` File` section. This file must be
included in the root directory of the repository of every PyAnsys library.

Project Approval
================
Exposing new Ansys technologies through the PyAnsys project is subject
to an internal review and decision process. Please reach out to
Stephane Marguerin or Alexander Kaszynski for any requests.


Repository Management and Standards
===================================
Each PyAnsys repository should at the minimum be administrated by a
single individual with "Admin" permissions over the repository. This
enables them to override any blocking pull requests or to change the
settings for that repository, such as GitHub pages, repository
description, or branch protection management.

Each repository is expected to follow this minimum set of standards:

- PEP8 code standards. See :ref:`PEP 8 Best Practices`.
- CI/CD using GitHub actions or Azure DevOps to enforce coding standards.
- Publicly hosted documentation describing the API and providing examples. See
  :ref:`API Documentation Style`.
- Unit testing with at least 80% test coverage.
- Infrastructure in place to deploy the library as a package on `PyPI`_. See :ref:`Packaging Style`.
- Proper license file and author. See :ref:`The \`\`setup.py\`\` File` and :ref:`The \`\`LICENSE\`\` File`.


Release Procedures and Versioning
=================================
PyAnsys library releases are managed through both automated
and manual review processes.

PyAnsys follows the `Semantic Versioning`_ process as closely as
possible:

* **Major** version when you make incompatible API changes.
* **Minor** version when you add functionality in a backwards compatible manner.
* **Patch** version when you make backwards compatible bug fixes.

One exception exists. MAJOR versions are not expected to be regularly
released when any incompatible API changes are made. They are only expected to
be released with major, globally-breaking API changes. This matches the
versioning methodology for the "big three" data science python libraries: `NumPy`_,
`SciPy`_, and `pandas`_.

Release Definition
------------------

**Major**

Major releases denote global, major breaking API changes. Adding or
changing a feature is not considered a globally-backwards incompatible
API change. Rather, a major release and version bump should be made
if globally-breaking changes are made that will require a
significant refactor of any dependent modules.

Note that ``0.MINOR.PATCH`` packages are expected to have fluid
APIs and should be solidified at the ``1.MINOR.PATCH`` release. At
that point, APIs are expected to be much more stable.

**Minor**

Minor releases are feature releases that improve the functionality and
stability of a PyAnsys library.

**Patch**

Patch releases are for critical and important bug fixes that cannot or
should not wait until a minor release.


Release Management
------------------
A release may be a major, minor, or patch release depending on the
features, changes, or bug fixes to be released.

For more information, see :ref:`Release Procedures`.


Product Version Matching
------------------------
PyAnsys libraries should not match product versions. For example, the
`PyMAPDL`_ library ``ansys-mapdl-core`` might have the version ``0.59.0``
whereas the product version is 21.2 (2021 R2). The reason
behind this is PyAnsys libraries are expected to be developed outside
the product release cycle in a rapid CI/CD manner.

.. LINKS AND REFERENCES
.. include:: ../links.rst
