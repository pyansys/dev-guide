Project Structure
#################

Most of the projects in the PyAnsys ecosystem ship in the form of a Python
library with other additional files. All these files form what it is called a
"project". A project can be uploaded to a repository to better track the changes
applied to it.


Naming Convention
=================

Large organizations providing Python packages follow a consistent naming
pattern. Ansys follows two naming conventions, depending on the nature of the project.

PyAnsys Library
---------------

- The project name is to be ``Py<project>``. For example, ``PyMAPDL`` is the
  project name for MAPDL and ``PyAEDT`` is the project name for AEDT.

- The repository name as hosted on GitHub should be all lowercase to follow
  GitHub community standards. For example, `pymapdl`_ and `pyaedt`_.

- The Python library name is to be in the format
  ``ansys-<product/service>-<feature>``. For example, `ansys-mapdl-core
  <https://pypi.org/project/ansys-mapdl-core/>`_ is the name for the core MAPDL
  library.

.. include:: diag/pyansys_namespace_diag.rst

The previous structure leads to the following namespace when executing the import
statement:

.. code:: python

   import ansys.product import library

Using long Python library names provides two primary advantages:

- `Namespace Packages`_ can be used to designate official Ansys packages.
- Consistent branding and style can be applied to PyAnsys libraries.


gRPC Interface Package
----------------------
Lower-level gRPC interface packages like `ansys-api-mapdl`_ should always be
named ``ansys-api-<product/service>`` and may contain an additional level:
``ansys-api-<product/service>-<secondlevel>``.

.. include:: diag/grpc_structure_diag.rst

This structure leads to the following namespace within ``*.proto`` files:

.. code::

   package ansys.api.<product/service>.v0;


Python Libraries
================

A Python library is the formal way of distributing Python source code. It allows
for reuse and for specifying Python code dependencies. The guidance presented in this section
is compliant with the `Python Packaging Authority`_ and PyAnsys recommendations.

.. note::

   The best way to keep up to date with Python packaging is to check the `Python
   Packaging User Guide`_, maintained by the `Python Packaging Authority`_ (PyPA).
   PyAnsys guidelines are built on top of PyPA guidelines.


Scripts, Modules, Sub-packages, and Packages
--------------------------------------------

To understand the structure of a Python Library, it is important to know
the difference between Python scripts, modules, sub-packages, and packages.

* ``Script``: Any Python file with logic source code
* ``Module``: Any Python script hosted next to an ``__init__.py`` file
* ``Sub-package``: Any directory containing various Python modules
* ``Package``: Any directory containing Python modules and sub-packages


Differences Between a Python Package and Library
------------------------------------------------

Although the terms *package* and *library* are often used interchangeably, there is
a key difference between them. A Python package is a collection of Python modules and
sub-packages, while a Python Library is a collection of Python packages. Figure
:numref:`python pkg lib diag` exposes this.

.. include:: diag/python_library_diag.rst


Required Files for a PyAnsys Project
====================================

The structure of any PyAnsys library contains these files and directories:

.. include:: diag/pyproduct_library_structure_diag.rst

Descriptions follow for some of the directories in the structure:

- ``doc/`` contains files related to documentation, guidelines, and examples.

- ``src/`` contains all Python modules and scripts that form the project.

- ``tests/`` contains all unit tests for checking the integrity of the project.

- ``setup.py`` or ``pyproject.toml`` is the project file.


The ``doc/`` Directory
----------------------

When distributing software, it is important to document it. Documenting software
means giving guidelines on how to install it and describing all functions,
methods, and classes that it ships with. Case scenarios and examples should also
be part of the documentation. 

A PyAnsys project should have the following documentation sections:

- ``Getting Started``: Defines requirements and provides installation information
- ``User Guide``: Explains how to use the software
- ``API Reference``: Describes the source code
- ``Examples``: Provides use case scenarios that demonstrate the capabilities of the software
- ``Contributing``: Supplies project-specific contribution guides and can link to general PyAnsys contribution guidelines

Projects in the PyAnsys ecosystem take advantage of `Sphinx`_, a tool used for
building documentation for Python-based projects. As shown in :numref:`doc structure diag`,
`Sphinx`_ requires a ``doc/`` directory with a specific structure:


.. include:: diag/doc_structure_diag.rst

- ``_build`` contains the rendered documentation in various formats, such as HTML
  and PDF.

- ``source`` contains the RST files that will be rendered when building the
  documentation.

- ``make.bat`` and ``Makefile`` are used to automate cleaning and building
  commands. You use ``make.bat`` when running on Windows and ``Makefile``
  when running on MacOS or Linux.

The ``source/`` directory must contain at least these files:

- ``conf.py`` is a Python script used to declare the configuration of `Sphinx`_.
- ``index.rst`` is the index page of the documentation. In this file, try to reuse the
  ``README.rst`` file to avoid duplication.

If you would like to include images or documents, add them in the ``_static/``
directory.


The ``src/`` Directory
----------------------

All the Python source code must be located in the ``src/`` directory. This is where the
build system will look when generating the wheel and source distributions.

.. warning::

   Folders inside the ``src/`` directory cannot contain spaces or hyphens. Replace these
   characters with an underscore '_'.

The structure of the ``src/`` directory determines the namespace of the PyAnsys
library. A namespace allow you to easily split sub-packages from a package into
single, independent distributions.

There are different approaches available for creating a namespace package. For
the Ansys namespace, we use the `PEP 420`_ `native namespace packages`_ approach.

Therefore, the source directory of any PyAnsys library must look like the one
shown in diagram :numref:`src structure diag`:

.. include:: diag/src_structure_diag.rst


The ``tests/`` Directory
------------------------

To guarantee the integrity of a PyAnsys project, a good test suite is required.
PyAnsys projects use the `pytest`_ testing framework.

A good practice is to emulate the structure of the ``src/ansys/product/library``
directory, although this is not always necessary.

.. include:: diag/tests_structure_diag.rst

Notice the use of ``tests_*/`` when creating new directories inside the
``tests/`` one. For unit testing files, names use the ``test_*.py`` prefix.
This is the preferred way of naming directories and files inside the
``tests/`` directory.


The ``LICENSE`` File
--------------------

The ``LICENSE`` file provides the legal framework for the software. `PyAnsys`_ 
projects must use `MIT License`_. A template for
this license is provided below:

.. include:: code/license_mit_code.rst

.. note::

   Just because a software does not ship with a LICENSE file, it does not mean
   it is free or open source. If you need to use unlicensed software, contact
   its development team so they can provide you with the correct license.


The ``README.rst`` File
-----------------------

Each PyAnsys library should have a ``README.rst`` file in the root directory.

The preferred format of this file is `reStructuredText Markup Syntax`_,
although `Markdown Syntax`_ can be used too.  While Markdown syntax has better
GitHub support, ReStructured Text (RST) files can be reused within Sphinx documentation.
This avoids duplication between the ``README.rst`` and the main ``index.rst`` in
the ``doc/source/`` directory.

The ``README.rst`` file should at the minimum contain these elements:

- PyAnsys library title
- General description
- Installation directions (via ``pip install`` and ``git clone``)
- Basic usage
- Links to the full documentation

The ``README.rst`` file is also reused within the project file metadata. It is
usually included in the ``long-description`` field.


The ``pyproject.toml`` File
---------------------------

`PEP 518`_ introduced the usage of a project file named
``pyproject.toml``.

The ``pyproject.toml`` file is mandatory because it allows ``pip`` to resolve the
requirements for building the library. The following tabs expose the ``[build-system]`` section
for some of the most popular build-system backend tools in the Python ecosystem:

.. include:: code/pyproject_code.rst


The ``setup.py`` File
---------------------

For a long time, the ``setup.py`` file was generally used to build and
distribute Python libraries. Unlike a static ``pyproject.toml`` file, the
``setup.py`` file is a Python script. This means that Python code is interpreted
when building the library. This approach supports customizing the build
process but can also introduce security issues.

.. note::

   The ``setup.py`` is only compatible with `setuptools`_. Consider using a
   ``pyproject.toml`` file instead.


While a ``setup.cfg`` file can be used to specify the metadata and packages, the ``setup.py``
file must also be present. For more information, see:

* `Building and Distributing Packages with Setuptools`_
* `Configuring setuptools using setup.cfg files`_

As a minimum configuration for a PyAnsys project, the following ``setup.py``
template can be used:


.. include:: code/setup_file_code.rst


.. REFERENCES & LINKS
.. include:: ../links.rst

.. _Building and Distributing Packages with Setuptools: https://setuptools.pypa.io/en/latest/setuptools.html
.. _Configuring setuptools using setup.cfg files: https://setuptools.pypa.io/en/latest/userguide/declarative_config.html
.. _Markdown Syntax: https://www.markdownguide.org/basic-syntax/
.. _Namespace Packages: https://packaging.python.org/guides/packaging-namespace-packages/
.. _native namespace packages: https://packaging.python.org/en/latest/guides/packaging-namespace-packages/#native-namespace-packages
.. _reStructuredText Markup Syntax: https://docutils.sourceforge.io/rst.html
