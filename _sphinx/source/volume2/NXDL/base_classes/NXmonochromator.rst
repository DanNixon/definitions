..  _NXmonochromator:

###############
NXmonochromator
###############

.. index::  ! . NXDL base_classes; NXmonochromator

category:
    base_classes

NXDL source:
    NXmonochromator
    
    (http://svn.nexusformat.org/definitions/trunk/base_classes/NXmonochromator.nxdl.xml)

version:
    1.0

SVN Id:
    $Id$

extends class:
    :ref:`NXobject`

other classes included:
    :ref:`NXcrystal`, :ref:`NXdata`, :ref:`NXgeometry`, :ref:`NXvelocity_selector`

documentation:
    This is a base class for everything which
    selects a wavelength or energy, be it a monochromator crystal, a velocity selector,
    a undulator or whatever.
    
    The expected units are:
    
    wavelength: angstrom
    
    energy:     eV
    


.. rubric:: Basic Structure of **NXmonochromator**

.. code-block:: text
    :linenos:
    
    NXmonochromator (base class, version 1.0)
      energy:NX_FLOAT
      energy_error:NX_FLOAT
      wavelength:NX_FLOAT
      wavelength_error:NX_FLOAT
      NXcrystal
      distribution:NXdata
      geometry:NXgeometry
      NXvelocity_selector
    

.. rubric:: Symbols used in definition of **NXmonochromator**

No symbols are defined in this NXDL file





.. rubric:: Comprehensive Structure of **NXmonochromator**

+---------------------+----------+-------+-------------------------------+
| Name and Attributes | Type     | Units | Description (and Occurrences) |
+=====================+==========+=======+===============================+
| class               | NX_FLOAT | ..    | ..                            |
+---------------------+----------+-------+-------------------------------+
