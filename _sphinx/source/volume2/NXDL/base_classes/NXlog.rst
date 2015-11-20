..  _NXlog:

#####
NXlog
#####

.. index::  ! . NXDL base_classes; NXlog

category:
    base_classes

NXDL source:
    NXlog
    
    (http://svn.nexusformat.org/definitions/trunk/base_classes/NXlog.nxdl.xml)

version:
    1.0

SVN Id:
    $Id$

extends class:
    :ref:`NXobject`

other classes included:
    none

documentation:
    Definition of information that is recorded against time,
    such as information monitored during the run.
    It contains
    the logged values and the times at which they were measured as elapsed time since a starting
    time recorded in ISO8601 format. This method of storing logged data helps to distinguish
    instances in which a variable is a dimension scale of the data, in which case it is stored
    in an NXdata group, and instances in which it is logged during the
    run, when it should be stored in an NXlog group.
    Note: When using multiple NXlog groups, it is suggested to place
    them inside a NXcollection group.  In such cases, when
    NXlog is used in another class,
    NXcollection/NXlog
    is then constructed.
    


.. rubric:: Basic Structure of **NXlog**

.. code-block:: text
    :linenos:
    
    NXlog (base class, version 1.0)
      average_value:NX_FLOAT
      average_value_error:NX_FLOAT
      description:NX_CHAR
      duration:NX_FLOAT
      maximum_value:NX_FLOAT
      minimum_value:NX_FLOAT
      raw_value:NX_NUMBER
      time:NX_FLOAT
        @start
      value:NX_NUMBER
    

.. rubric:: Symbols used in definition of **NXlog**

No symbols are defined in this NXDL file





.. rubric:: Comprehensive Structure of **NXlog**

+---------------------+----------+-------+-------------------------------+
| Name and Attributes | Type     | Units | Description (and Occurrences) |
+=====================+==========+=======+===============================+
| class               | NX_FLOAT | ..    | ..                            |
+---------------------+----------+-------+-------------------------------+
