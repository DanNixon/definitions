.. $Id$

.. _Introduction-HowToRead:

How do I read a NeXus file?
---------------------------------------------------------------------------------

.. index:: file; read
.. index:: NAPI
.. index:: rank

Reading a NeXus file is almost identical to writing one. Obviously, it is not
necessary to call ``NXmakedata()`` 
since the item already exists, but it
is necessary to call one of the query routines to find out the rank
and length of the data before allocating an array to store it.

Here is part of a program to read the two-theta array from the file
created by :ref:`ex.simple.write` above.

.. _ex.simple.read:

Reading a simple NeXus file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. index:: example; simple

.. code-block:: text
	:linenos: 

	 NXopen ('NXfile.nxs', NXACC_READ, &fileID);
	   NXopengroup (fileID, "Scan", "NXentry");
		 NXopengroup (fileID, "data", "NXdata");
		   NXopendata (fileID, "two_theta");
			 NXgetinfo (fileID, &rank, dims, &datatype);
			 NXmalloc ((void **) &tth, rank, dims, datatype);
			 NXgetdata (fileID, tth);
		   NXclosedata (fileID);
		 NXclosegroup (fileID);
	   NXclosegroup (fileID);
	 NXclose (fileID);
