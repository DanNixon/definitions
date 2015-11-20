.. $Id$

.. _Introduction-HowToBrowse:

How do I browse a NeXus file?
---------------------------------------------------------------------------------

.. index:: file; browse
.. index:: utility; nxbrowse

NeXus files can also be viewed by a command-line browser,
``NXbrowse``, which is included with the NeXus API (:ref:`Introduction-NAPI`).
The following is an example session of using ``nxbrowse``
to view a data
file from the LRMECS spectrometer at IPNS. The following commands 
are used in :ref:`ex.NXbrowse.lrmecs` in this session (see
the ``nxbrowse`` web page):

.. _ex.NXbrowse.lrmecs:

Using ``NXbrowse``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: text
	:linenos: 

	%> nxbrowse lrcs3701.nxs

	NXBrowse 3.0.0. Copyright (C) 2000 R. Osborn, M. Koennecke, P. Klosowski
		NeXus_version = 1.3.3
		file_name = lrcs3701.nxs
		file_time = 2001-02-11 00:02:35-0600
		user = EAG/RO
	NX> dir
	  NX Group : Histogram1 (NXentry)
	  NX Group : Histogram2 (NXentry)
	NX> open Histogram1
	NX/Histogram1> dir
	  NX Data  : title[44] (NX_CHAR)
	  NX Data  : analysis[7] (NX_CHAR)
	  NX Data  : start_time[24] (NX_CHAR)
	  NX Data  : end_time[24] (NX_CHAR)
	  NX Data  : run_number (NX_INT32)
	  NX Group : sample (NXsample)
	  NX Group : LRMECS (NXinstrument)
	  NX Group : monitor1 (NXmonitor)
	  NX Group : monitor2 (NXmonitor)
	  NX Group : data (NXdata)
	NX/Histogram1> read title
	  title[44] (NX_CHAR) = MgB2 PDOS 43.37g 8K 120meV E0@240Hz T0@120Hz
	NX/Histogram1> open data
	NX/Histogram1/data> dir
	  NX Data  : title[44] (NX_CHAR)
	  NX Data  : data[148,750] (NX_INT32)
	  NX Data  : time_of_flight[751] (NX_FLOAT32)
	  NX Data  : polar_angle[148] (NX_FLOAT32)
	NX/Histogram1/data> read time_of_flight
	  time_of_flight[751] (NX_FLOAT32) = [ 1900.000000 1902.000000 1904.000000 ...]
		units = microseconds
		long_name = Time-of-Flight [microseconds]
	NX/Histogram1/data> read data
	  data[148,750] (NX_INT32) = [ 1 1 0 ...]
		units = counts
		signal = 1 
		long_name = Neutron Counts
		axes = polar_angle:time_of_flight
	NX/Histogram1/data> close
	NX/Histogram1> close
	NX> quit

.. index:: example; simple

[line 1]
	Start ``NXbrowse`` from the UNIX command 
	line and open file ``lrcs3701.nxs`` from 
	IPNS/LRMECS.
[line 8] 
	List the contents of the current group.
[line 11]
	Open the NeXus group ``Histogram1``.
[line 23]
	Print the contents of the NeXus data labelled ``title``.
[line 41] 
	Close the current group.
[line 43] 
	Quits ``NXbrowse``.

The source code of ``NXbrowse`` [#]_
provides an example of how to write a NeXus reader. 
The test programs included in the NeXus API (:ref:`Introduction-NAPI`)
may also be useful to study.

.. [#] https://svn.nexusformat.org/code/trunk/applications/NXbrowse/NXbrowse.c
