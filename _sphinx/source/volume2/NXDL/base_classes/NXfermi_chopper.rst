..  _NXfermi_chopper:

###############
NXfermi_chopper
###############

.. index::  ! . NXDL base_classes; NXfermi_chopper

category:
    base_classes

NXDL source:
    NXfermi_chopper
    
    (http://svn.nexusformat.org/definitions/trunk/base_classes/NXfermi_chopper.nxdl.xml)

version:
    1.0

SVN Id:
    $Id$

extends class:
    :ref:`NXobject`

other classes included:
    :ref:`NXgeometry`

documentation:
    Description of a Fermi chopper, possibly with curved slits.
    


.. rubric:: Basic Structure of **NXfermi_chopper**

.. code-block:: text
    :linenos:
    
    NXfermi_chopper (base class, version 1.0)
      absorbing_material:NX_CHAR
      distance:NX_FLOAT
      energy:NX_FLOAT
      height:NX_FLOAT
      number:NX_INT
      r_slit:NX_FLOAT
      radius:NX_FLOAT
      rotation_speed:NX_FLOAT
      slit:NX_FLOAT
      transmitting_material:NX_CHAR
      type:NX_CHAR
      wavelength:NX_FLOAT
      width:NX_FLOAT
      NXgeometry
    

.. rubric:: Symbols used in definition of **NXfermi_chopper**

No symbols are defined in this NXDL file





.. rubric:: Comprehensive Structure of **NXfermi_chopper**

+---------------------+----------+-------+-------------------------------+
| Name and Attributes | Type     | Units | Description (and Occurrences) |
+=====================+==========+=======+===============================+
| class               | NX_FLOAT | ..    | ..                            |
+---------------------+----------+-------+-------------------------------+
