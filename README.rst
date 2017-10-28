Technical notes
===============

This repository contains a set of technical notes in various software
engineering areas. The notes are formatted as RST documentation which can be
rendered to static web site by `Sphinx <http://www.sphinx-doc.org>`_.

Usage
-----

#. Generate static HTML

.. code-block:: bash

    git clone git@github.com:ivankliuk/tech-notes.git
    cd tech-notes/
    sphinx-build -b html . docs/

#. Run local HTTP server on 8000

.. code-block:: bash

    cd docs/
    python -m SimpleHTTPServer
