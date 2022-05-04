API Documentation Style
#######################
Good API documentation drives library adoption and usage and is the
foundation for a good developer experience.  Even with the best
interfaces and the most functional product, no one will adopt the API
if they don't know how to use it or if they aren't satisfied with the
documentation or examples that they are presented with.

Good API documentation provides:

* Increased adoption and improved experiences for developers using
  the API or library.
* Reduction in the time spent on-boarding new contributors and users
  of the library.
* Better maintenance of the code base. The time spent reading the
  source is often orders of magnitude greater than the time spent
  writing it. Well documented code (both in user-facing docstrings
  and developer comments) pays dividends in code maintenance.
* Reduction in the amount of time spent understanding the API features.

The documentation for a PyAnsys library should contain:

* Module, class, method, and function docstrings. See 
  :ref:`docstrings`.
* Full gallery of examples. See `PyMAPDL Examples`_.
* Developer's guide for the library.
* Link to this developer's guide.

Finally, the documentation should be public and hosted via gh-pages, either as
a branch named ``gh-pages`` within the library repository or within a
``gh-pages`` branch within ``<library-repository>-docs``. For more information,
see :ref:`Documentation Deployment`.

.. toctree::
   :hidden:
   :maxdepth: 3

   docstrings
   class_documentation
   deployment
   formatting-tools

.. Links and References
.. include:: ../links.rst
