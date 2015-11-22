..  _NXsnshisto:

##########
NXsnshisto
##########

.. index::  ! . NXDL contributed_definitions; NXsnshisto

category:
    contributed_definitions

NXDL source:
    NXsnshisto
    
    (http://svn.nexusformat.org/definitions/trunk/contributed_definitions/NXsnshisto.nxdl.xml)

version:
    1.0

SVN Id:
    $Id$

extends class:
    :ref:`NXobject`

other classes included:
    :ref:`NXaperture`, :ref:`NXattenuator`, :ref:`NXcollection`, :ref:`NXcrystal`, :ref:`NXdata`, :ref:`NXdetector`, :ref:`NXdisk_chopper`, :ref:`NXentry`, :ref:`NXfermi_chopper`, :ref:`NXgeometry`, :ref:`NXinstrument`, :ref:`NXlog`, :ref:`NXmoderator`, :ref:`NXmonitor`, :ref:`NXnote`, :ref:`NXorientation`, :ref:`NXpolarizer`, :ref:`NXpositioner`, :ref:`NXsample`, :ref:`NXshape`, :ref:`NXsource`, :ref:`NXtranslation`, :ref:`NXuser`

documentation:
    This is a definition for histogram data from Spallation Neutron Source (SNS) at ORNL.
    


.. rubric:: Basic Structure of **NXsnshisto**

.. code-block:: text
    :linenos:
    
    NXsnshisto (contributed definition, version 1.0)
      (overlays NXentry)
      NXentry
        collection_identifier:NX_CHAR
        collection_title:NX_CHAR
        definition:NX_CHAR
        duration:NX_FLOAT
        end_time:NX_DATE_TIME
        entry_identifier:NX_CHAR
        experiment_identifier:NX_CHAR
        notes:NX_CHAR
        proton_charge:NX_FLOAT
        raw_frames:NX_INT
        run_number:NX_CHAR
        start_time:NX_DATE_TIME
        title:NX_CHAR
        total_counts:NX_UINT
        total_uncounted_counts:NX_UINT
        DASlogs:NXcollection
          NXlog
            average_value:NX_FLOAT
            average_value_error:NX_FLOAT
            description:NX_CHAR
            duration:NX_FLOAT
            maximum_value:NX_FLOAT
            minimum_value:NX_FLOAT
            time:NX_FLOAT[nvalue]
            value:NX_FLOAT[nvalue]
          NXpositioner
            average_value:NX_FLOAT
            average_value_error:NX_FLOAT
            description:NX_CHAR
            duration:NX_FLOAT
            maximum_value:NX_FLOAT
            minimum_value:NX_FLOAT
            time:NX_FLOAT[numvalue]
            value:NX_FLOAT[numvalue]
        NXdata
          data --> /NXentry/NXinstrument/NXdetector/data
          data_x_time_of_flight --> /NXentry/NXinstrument/NXdetector/data_x_time_of_flight
          data_x_y --> /NXentry/NXinstrument/NXdetector/data_x_y
          data_y_time_of_flight --> /NXentry/NXinstrument/NXdetector/data_y_time_of_flight
          pixel_id --> /NXentry/NXinstrument/NXdetector/pixel_id
          time_of_flight --> /NXentry/NXinstrument/NXdetector/time_of_flight
          total_counts --> /NXentry/NXinstrument/NXdetector/total_counts
          x_pixel_offset --> /NXentry/NXinstrument/NXdetector/x_pixel_offset
          y_pixel_offset --> /NXentry/NXinstrument/NXdetector/y_pixel_offset
        instrument:NXinstrument
          SNSdetector_calibration_id:NX_CHAR
          SNSgeometry_file_name:NX_CHAR
          SNStranslation_service:NX_CHAR
          beamline:NX_CHAR
          name:NX_CHAR
          NXaperture
            x_pixel_offset:NX_FLOAT
            origin:NXgeometry
              orientation:NXorientation
                value:NX_FLOAT[6]
              shape:NXshape
                description:NX_CHAR
                shape:NX_CHAR
                size:NX_FLOAT[3]
              translation:NXtranslation
                distance:NX_FLOAT[3]
          NXattenuator
            distance:NX_FLOAT
          NXcrystal
            type:NX_CHAR
            wavelength:NX_FLOAT
            origin:NXgeometry
              description:NX_CHAR
              orientation:NXorientation
                value:NX_FLOAT[6]
              shape:NXshape
                description:NX_CHAR
                shape:NX_CHAR
                size:NX_FLOAT
              translation:NXtranslation
                distance:NX_FLOAT[3]
          NXdetector
            azimuthal_angle:NX_FLOAT[numx,numy]
            data:NX_UINT[numx,numy,numtof]
            data_x_time_of_flight:NX_UINT[numx,numtof]
            data_x_y:NX_UINT[numx,numy]
            data_y_time_of_flight:NX_UINT[numy,numtof]
            distance:NX_FLOAT[numx,numy]
            pixel_id:NX_UINT[numx,numy]
            polar_angle:NX_FLOAT[numx,numy]
            time_of_flight:NX_FLOAT[numtof + 1]
            total_counts:NX_UINT
            x_pixel_offset:NX_FLOAT[numx]
            y_pixel_offset:NX_FLOAT[numy]
            origin:NXgeometry
              orientation:NXorientation
                value:NX_FLOAT[6]
              shape:NXshape
                description:NX_CHAR
                shape:NX_CHAR
                size:NX_FLOAT[3]
              translation:NXtranslation
                distance:NX_FLOAT[3]
          NXdisk_chopper
            distance:NX_FLOAT
          NXfermi_chopper
            distance:NX_FLOAT
          moderator:NXmoderator
            coupling_material:NX_CHAR
            distance:NX_FLOAT
            temperature:NX_FLOAT
            type:NX_CHAR
          NXpolarizer
          SNS:NXsource
            frequency:NX_FLOAT
            name:NX_CHAR
            probe:NX_CHAR
            type:NX_CHAR
        NXmonitor
          data:NX_UINT[numtimechannels]
          distance:NX_FLOAT
          mode:NX_CHAR
          time_of_flight:NX_FLOAT[numtimechannels + 1]
        SNSHistoTool:NXnote
          SNSbanking_file_name:NX_CHAR
          SNSmapping_file_name:NX_CHAR
          author:NX_CHAR
          command1:NX_CHAR
          date:NX_CHAR
          description:NX_CHAR
          version:NX_CHAR
        sample:NXsample
          changer_position:NX_CHAR
          holder:NX_CHAR
          identifier:NX_CHAR
          name:NX_CHAR
          nature:NX_CHAR
        NXuser
          facility_user_id:NX_CHAR
          name:NX_CHAR
          role:NX_CHAR
    

.. rubric:: Symbols used in definition of **NXsnshisto**

No symbols are defined in this NXDL file





.. rubric:: Comprehensive Structure of **NXsnshisto**

+---------------------+----------+-------+-------------------------------+
| Name and Attributes | Type     | Units | Description (and Occurrences) |
+=====================+==========+=======+===============================+
| class               | NX_FLOAT | ..    | ..                            |
+---------------------+----------+-------+-------------------------------+
