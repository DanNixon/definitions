..  _NXorientation:

#############
NXorientation
#############

.. index::  ! . NXDL base_classes; NXorientation

category:
    base_classes

NXDL source:
    NXorientation
    
    (http://svn.nexusformat.org/definitions/trunk/base_classes/NXorientation.nxdl.xml)

version:
    1.0

SVN Id:
    $Id$

extends class:
    :ref:`NXobject`

other classes included:
    :ref:`NXgeometry`

documentation:
    This is the description for a general orientation of a component - it is used by the
    NXgeometry class
    


.. rubric:: Basic Structure of **NXorientation**

.. code-block:: text
    :linenos:
    
    NXorientation (base class, version 1.0)
      value:NX_FLOAT[numobj,6]
      NXgeometry
    

.. rubric:: Symbols used in definition of **NXorientation**

No symbols are defined in this NXDL file





.. rubric:: Comprehensive Structure of **NXorientation**

+---------------------+----------+-------+-------------------------------+
| Name and Attributes | Type     | Units | Description (and Occurrences) |
+=====================+==========+=======+===============================+
| class               | NX_FLOAT | ..    | ..                            |
+---------------------+----------+-------+-------------------------------+
