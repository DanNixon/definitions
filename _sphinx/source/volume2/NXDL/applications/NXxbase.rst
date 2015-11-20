..  _NXxbase:

#######
NXxbase
#######

.. index::  ! . NXDL applications; NXxbase

category:
    applications

NXDL source:
    NXxbase
    
    (http://svn.nexusformat.org/definitions/trunk/applications/NXxbase.nxdl.xml)

version:
    1.0b

SVN Id:
    $Id$

extends class:
    :ref:`NXobject`

other classes included:
    :ref:`NXdata`, :ref:`NXdetector`, :ref:`NXentry`, :ref:`NXinstrument`, :ref:`NXmonitor`, :ref:`NXmonochromator`, :ref:`NXsample`, :ref:`NXsource`

documentation:
    This definition covers the common parts of all monochromatic
    single crystal raw data application definitions
    


.. rubric:: Basic Structure of **NXxbase**

.. code-block:: text
    :linenos:
    
    NXxbase (application definition, version 1.0b)
      (overlays NXentry)
      entry:NXentry
        definition:NX_CHAR
        start_time:NX_DATE_TIME
        title:NX_CHAR
        NXdata
          data --> /NXentry/NXinstrument/NXdetector/data
        instrument:NXinstrument
          detector:NXdetector
            data:NX_INT[np,number of x pixels,number of y pixels]
              @signal
            distance:NX_FLOAT
            frame_start_number:NX_INT
            x_pixel_size:NX_FLOAT
            y_pixel_size:NX_FLOAT
          monochromator:NXmonochromator
            wavelength:NX_FLOAT
          source:NXsource
            name:NX_CHAR
            probe:NX_CHAR
            type:NX_CHAR
        control:NXmonitor
          integral:NX_FLOAT
          mode:NX_CHAR
          preset:NX_FLOAT
        sample:NXsample
          distance:NX_FLOAT
          name:NX_CHAR
          orientation_matrix:NX_FLOAT[3,3]
          temperature:NX_FLOAT[NP]
          unit_cell:NX_FLOAT[6]
          x_translation:NX_FLOAT
          y_translation:NX_FLOAT
    

.. rubric:: Symbols used in definition of **NXxbase**

No symbols are defined in this NXDL file





.. rubric:: Comprehensive Structure of **NXxbase**

+---------------------+----------+-------+-------------------------------+
| Name and Attributes | Type     | Units | Description (and Occurrences) |
+=====================+==========+=======+===============================+
| class               | NX_FLOAT | ..    | ..                            |
+---------------------+----------+-------+-------------------------------+
