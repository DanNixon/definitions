.. $Id$

.. _Introduction-HowToWrite:

How do I write a NeXus file?
---------------------------------------------------------------------------------

.. index:: file; write
.. index:: NAPI

The NeXus Application Program Interface (API) 
provides a set of subroutines that make it easy to read and write
NeXus files. These subroutines are available in C, Fortran 77, Fortran 90, Java,
Python, C++,
and IDL. Access from other languages, such as Python, is anticipated in the near
future. It is also possible to read NeXus HDF files in a number of data analysis
tools, such as LAMP, ISAW, IgorPro, and Open GENIE.  NeXus XML files can be read 
by any program or library that supports XML.

The API uses a very simple *state*
model to navigate through a NeXus file.
When you open a file, the API provides a file *handle*, 
which then stores the
current location, i.e. which group and/or field is currently open. Read and
write operations then act on the currently open entity. 
Following the :ref:`fig.simple-example`,
we walk through some parts of a typical NeXus program written in C.

.. _ex.simple.write:

Writing a simple NeXus file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. index:: example; simple
.. code-block:: text
	:linenos: 

	#include "napi.h"

	 int main()
	 {
		NXhandle fileID;
		NXopen ('NXfile.nxs', NXACC_CREATE, &fileID);
		  NXmakegroup (fileID, "Scan", "NXentry");
		  NXopengroup (fileID, "Scan", "NXentry");
			NXmakegroup (fileID, "data", "NXdata");
			NXopengroup (fileID, "data", "NXdata");
			/* somehow, we already have arrays tth and counts, each length n*/
			  NXmakedata (fileID, "two_theta", NX_FLOAT32, 1, &n);
			  NXopendata (fileID, "two_theta");
				NXputdata (fileID, tth);
				NXputattr (fileID, "units", "degrees", 7, NX_CHAR);
			  NXclosedata (fileID);  /* two_theta */, NX_INT32, 1, &n);
			  NXopendata (fileID, "counts");
				NXputdata (fileID, counts);
			  NXclosedata (fileID);  /* counts */
			NXclosegroup (fileID);  /* data */
		  NXclosegroup (fileID);  /* Scan */
		NXclose (&fileID);
		return;
	}

[line 6]
	Open the file ``NXfile.nxs`` with 
	*create* 
	access (implying write access).
	NAPI returns a file identifier of type ``NXhandle``.

[line 7]
	Next, we create an
	``NXentry`` group to contain the scan using 
	``NXmakegroup()`` and then
	open it for access using ``NXopengroup()``.

[line 9]
	The plottable data
	is contained within an ``NXdata`` group, which must
	also be created and opened.

.. index:: NeXus basic motivation; default plot

[line 12]
	To create a field, call ``NXmakedata()``, specifying the
	data name, type (``NX_FLOAT32``), rank
	(in this case, 
	``1``), and length of the array
	(``n``). Then, it can be opened for writing.

.. index:: rank

[line 14]
	Write the data using ``NXputdata()``. 

[line 15]
	With the field still open, we can also add some data attributes,
	such as the data units,
	which are specified as a character string (type ``NX_CHAR``)
	that is 7 bytes long.

.. index:: attributes; data
.. index:: units

[line 16]
	Then we close the field before opening another. 
	In fact, the API will do this automatically if you 
	attempt to open another field, but it is
	better style to close it yourself. 

[line 17]
	The remaining fields in this group are added in a similar
	fashion. Note that the indentation whenever a new field or 
	group are opened is just intended to make the structure of
	the NeXus file more transparent.

[line 20]
	Finally, close the groups (``NXdata`` and 
	``NXentry``) before closing the file itself. 
