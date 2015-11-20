..  _NXinsertion_device:

##################
NXinsertion_device
##################

.. index::  ! . NXDL base_classes; NXinsertion_device

category:
    base_classes

NXDL source:
    NXinsertion_device
    
    (http://svn.nexusformat.org/definitions/trunk/base_classes/NXinsertion_device.nxdl.xml)

version:
    1.0

SVN Id:
    $Id$

extends class:
    :ref:`NXobject`

other classes included:
    :ref:`NXdata`, :ref:`NXgeometry`

documentation:
    Description of an insertion device, as in a synchrotron.
    


.. rubric:: Basic Structure of **NXinsertion_device**

.. code-block:: text
    :linenos:
    
    NXinsertion_device (base class, version 1.0)
      bandwidth:NX_FLOAT
      energy:NX_FLOAT
      gap:NX_FLOAT
      harmonic:NX_INT
      k:NX_FLOAT
      length:NX_FLOAT
      magnetic_wavelength:NX_FLOAT
      phase:NX_FLOAT
      poles:NX_INT
      power:NX_FLOAT
      taper:NX_FLOAT
      type:NX_CHAR
      spectrum:NXdata
      NXgeometry
    

.. rubric:: Symbols used in definition of **NXinsertion_device**

No symbols are defined in this NXDL file





.. rubric:: Comprehensive Structure of **NXinsertion_device**

+---------------------+----------+-------+-------------------------------+
| Name and Attributes | Type     | Units | Description (and Occurrences) |
+=====================+==========+=======+===============================+
| class               | NX_FLOAT | ..    | ..                            |
+---------------------+----------+-------+-------------------------------+
