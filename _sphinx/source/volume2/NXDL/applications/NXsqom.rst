..  _NXsqom:

######
NXsqom
######

.. index::  ! . NXDL applications; NXsqom

category:
    applications

NXDL source:
    NXsqom
    
    (http://svn.nexusformat.org/definitions/trunk/applications/NXsqom.nxdl.xml)

version:
    1.0b

SVN Id:
    $Id$

extends class:
    :ref:`NXobject`

other classes included:
    :ref:`NXdata`, :ref:`NXentry`, :ref:`NXinstrument`, :ref:`NXparameters`, :ref:`NXprocess`, :ref:`NXsample`, :ref:`NXsource`

documentation:
    This is the application definition for S(Q,OM) processed data. As this kind of data is in
    general not on a rectangular grid after data reduction, it is stored as Q,E positions plus their
    intensity, table like. It is the task of a possible visualisation program to regrid this data in
    a sensible way.
    


.. rubric:: Basic Structure of **NXsqom**

.. code-block:: text
    :linenos:
    
    NXsqom (application definition, version 1.0b)
      (overlays NXentry)
      NXentry
        @entry
        definition:NX_CHAR
        title:NX_CHAR
        NXdata
          data:NX_INT[NP]
          en:NX_FLOAT[NP]
          qx:NX_CHAR
          qy:NX_CHAR
          qz:NX_CHAR
        instrument:NXinstrument
          name:NX_CHAR
          NXsource
            name:NX_CHAR
            probe:NX_CHAR
            type:NX_CHAR
        reduction:NXprocess
          program:NX_CHAR
          version:NX_CHAR
          input:NXparameters
            filenames:NX_CHAR
          output:NXparameters
        NXsample
          name:NX_CHAR
    

.. rubric:: Symbols used in definition of **NXsqom**

No symbols are defined in this NXDL file





.. rubric:: Comprehensive Structure of **NXsqom**

+---------------------+----------+-------+-------------------------------+
| Name and Attributes | Type     | Units | Description (and Occurrences) |
+=====================+==========+=======+===============================+
| class               | NX_FLOAT | ..    | ..                            |
+---------------------+----------+-------+-------------------------------+
