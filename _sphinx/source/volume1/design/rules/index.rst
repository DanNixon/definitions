.. $Id$

.. _Rules:

================================================
Rules for Structuring Information in NeXus Files
================================================

.. index:: rules; NeXus
.. index:: rules; naming

All NeXus files contain one or many groups of type ``NXentry`` at root 
level. Many files contain only one ``NXentry`` group, then the name is 
``entry``. The NXentry level of hierarchy is there to support the storage 
of multiple related experiments in one file. Or to allow the NeXus file to 
serve as a container for storing a whole scientific workflow from data 
acquisition to publication ready data. Also, ``NXentry`` class groups can 
contain raw data or processed data. For files with more than one 
``NXentry`` group, since HDF requires that no two items at the same level 
in an HDF file may have the same name, the NeXus fashion is to assign 
names with an incrementing index appended, such as ``entry1``, ``entry2``, 
``entry3``, etc.       


In order to illustrate what is written in the text, 
example hierarchies like the one in 
figure <link xlink:href="#table.RawData">Raw Data</link> are provided.

.. _Rules-NXentry-raw-data:

Content of a Raw Data ``NXentry`` Group
---------------------------------------
      
An example raw data hierarchy is shown in the next figure (only showing 
the relevant parts of the data hierarchy). In the example shown, the 
``data`` field in the :ref:`NXdata` group is linked to the 2-D detector data 
(a 512x512 array of 32-bit integers) which has the attribute ``signal=1``. 
Note that ``[,]`` represents a 2D array.

.. code-block:: text
   :linenos:

   entry:NXentry
      instrument:NXinstrument
         source:NXsource
         ....
         detector:NXdetector
            data:NX_INT32[512,512]
               @signal = 1
      sample:NXsample
      control:NXmonitor
      data:NXdata
         data --> /entry/instrument/detector/data
     
An :ref:`NXentry` describing raw data contains at least a :ref:`NXsample`, one 
:ref:`NXmonitor`, one :ref:`NXdata` and a :ref:`NXinstrument` group. It is good 
practice to use the names ``sample`` for the :ref:`NXsample` group, 
``control`` for the :ref:`NXmonitor` group holding the experiment 
controlling monitor and ``instrument`` for the :ref:`NXinstrument` group. 
The :ref:`NXinstrument` group contains further groups describing the 
individual components of the instrument as appropriate.

.. index:: hierarchy

The ``NXdata`` group contains links to all those data items in the 
``NXentry`` hierarchy which are required to put up a default plot of the 
data.  As an example consider a SAXS instrument with a 2D detector. The 
``NXdata`` will then hold a link to the detector image.  If there is only 
one ``NXdata`` group, it is good practice to name it ``data``. Otherwise, 
the name of the detector bank represented is a good selection. 

.. TODO: show an example of this


.. include rules/processed   here
