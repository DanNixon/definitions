.. $Id$

.. _Introduction-NAPI:

=====================================================================
NAPI: The NeXus Application Programming Interface
=====================================================================

.. index:: NAPI

The NeXus API consists of routines to read and 
write NeXus data files and
was written to shield (and hide) the complexity
of the HDF API from scientific programmers and 
users of the NeXus Data Standard.

Further documentation of the NeXus Application Programming Interface
(NAPI) for bindings to specific programming language can be obtained
from the NeXus development site. [#]_

For a more detailed description of the internal workings of NAPI
that is maintained (mostly) concurrent with code revisions,
see the NAPI chapter in Volume II of this documentation and also 
`NeXusIntern.pdf <http://svn.nexusformat.org/code/trunk/doc/api/NeXusIntern.pdf>`_
in the NeXus code repository. [#]_
Likely this is only interesting for experienced
programmers who wish to hack the NAPI.

.. [#] http://download.nexusformat.org
.. [#] http://svn.nexusformat.org/code/trunk/doc/api/NeXusIntern.pdf

.. toctree::

    howto/write
    howto/read
    howto/browse

