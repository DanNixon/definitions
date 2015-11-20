..  _NXspin_rotator:

##############
NXspin_rotator
##############

.. index::  ! . NXDL contributed_definitions; NXspin_rotator

category:
    contributed_definitions

NXDL source:
    NXspin_rotator
    
    (http://svn.nexusformat.org/definitions/trunk/contributed_definitions/NXspin_rotator.nxdl.xml)

version:
    1.0

SVN Id:
    $Id$

extends class:
    :ref:`NXobject`

other classes included:
    :ref:`NXlog`

documentation:
    definition for a spin rotator.
    


.. rubric:: Basic Structure of **NXspin_rotator**

.. code-block:: text
    :linenos:
    
    NXspin_rotator (contributed definition, version 1.0)
      (base class definition, NXentry or NXsubentry not found)
      beamline_distance:NX_FLOAT
      description:NX_CHAR
      set_Bfield_current:NX_FLOAT
      set_Efield_voltage:NX_FLOAT
      read_Bfield_current:NXlog
        value:NX_CHAR
      read_Bfield_voltage:NXlog
        value:NX_CHAR
      read_Efield_current:NXlog
        value:NX_CHAR
      read_Efield_voltage:NXlog
        value:NX_CHAR
    

.. rubric:: Symbols used in definition of **NXspin_rotator**

No symbols are defined in this NXDL file





.. rubric:: Comprehensive Structure of **NXspin_rotator**

+---------------------+----------+-------+-------------------------------+
| Name and Attributes | Type     | Units | Description (and Occurrences) |
+=====================+==========+=======+===============================+
| class               | NX_FLOAT | ..    | ..                            |
+---------------------+----------+-------+-------------------------------+
