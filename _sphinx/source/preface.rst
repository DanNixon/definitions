.. $Id$

.. _preface:

Preface
=================================================

With this edition of the manual, NeXus introduces a complete version
of the documentation of the NeXus standard.  The content from the wiki
has been converted, augmented (in some parts significantly), clarified,
and indexed.  The NeXus Definition Language (NXDL) is introduced now
to define base classes and application definitions.  
NXDL replaces the previous method (meta-DTD) to define NeXus classes.
NeXus base classes and instrument definitions
are now assigned to one of three classifications: 

#. *base classes* (that represent the components used 
   to build a NeXus data file), 
#. *application definitions* (that define a minimum 
   set of data for a specific purpose such as scientific data processing
   or an instrument definition),
   and
#. *contributed definitions* (definitions and specifications
   that are in an incubation status before ratification by the NIAC).

Additional examples have been added to respond to
inquiry from the users of the NeXus standard about implementation
and usage.  Hopefully, the improved documentation with
more examples and the new NXDL will reduce
the learning barriers incurred by those new to NeXus.


Representation of data examples
-------------------------------------------------

.. index::
   single: data; examples

Most of the examples of data files have been written in a format
intended to show the structure of the file rather than the data content.
In some cases, where it is useful, some of the data is shown.
Consider this prototype example:

.. code-block:: text
	:linenos:

	entry:NXentry
		instrument:NXinstrument
			detector:NXdetector
				data:[]
					@axes = "bins"
					@long_name = "strip detector 1-D array"
					@signal = 1
				bins:[0, 1, 2, ... 1023]
					@long_name = "bin index numbers"
		sample:NXsample
			name = "zeolite"
		data:NXdata
			data --> /entry/instrument/detector/data
			bins --> /entry/instrument/detector/bins
   
Some words on the notation:

* Hierarchy is represented by indentation. 
  Objects on the same indentation level are in the same group
* The combination ``name:NXclass`` denotes a NeXus group with  
  name ``name`` and class ``NXclass``.
* A simple name (no following class) denotes a data field.  
  An equal sign is used to show the value, where this is 
  important to the example.
* Sometimes, a data type is specified and possibly a set of  
  dimensions. For example, ``energy:NX_NUMBER[NE]`` says ``energy``
  is a 1-D array of numbers (either integer or floating point)  
  of length ``NE``.
* Attributes are noted as ``@name=value`` pairs separated by comma.  
  The ``@`` symbol only indicates this is an attribute.  The ``@``
  symbol is not part of the attribute name.
* Links are shown with a text arrow ``-->`` indicating the source  
  of the link (using HDF5 notation listing the sequence of names).

[Line 1]
   shows that there is one group at the root level of the file named
   ``entry``.  This group is of type ``NXentry``
   which means it conforms to the specification of the ``NXentry``
   NeXus base class.  Using the HDF5 nomenclature, we would refer to this
   as the ``/entry`` group.

[Lines 2, 10, and 12]
   The ``/entry`` group contains three subgroups:
   ``instrument``, ``sample``, and ``data``.
   These groups are of type ``NXinstrument``, ``NXsample``,
   and ``NXdata``, respectively.

[Line 4]
   The data of this example is stored in the
   ``/entry/instrument/detector`` group in the dataset called
   ``data`` (HDF5 path is ``/entry/instrument/detector/data``).
   The indication of ``data:[]`` says that ``data`` is an
   array of unspecified dimension(s).

[Lines 5-7]
   There are three attributes of ``/entry/instrument/detector/data``:
   ``axes``, ``long_name``, and ``signal``.

[Line 8] (reading ``bins:[0, 1, 2, ... 1023]``) 
   shows that
   ``bins`` is a 1-D array of length presumably 1024.  A small,
   representative selection of values are shown.

[Line 9]
   an attribute that shows a descriptive name of
   ``/entry/instrument/detector/bins``.  This attribute
   might be used by a NeXus client while plotting the data.

[Line 11] (reading ``name = "zeolite"``) 
   shows how a string value is represented.

[Lines 13-14]
   The ``/entry/data`` group has two datasets that are actually
   linked as shown.  (As you will see later, the ``NXdata`` group
   is required and enables NeXus clients to easily determine what to
   offer for display on a default plot.)


Class path specification
-------------------------------------------------

In some places in this documentation, a path may be shown
using the class types rather than names.  For example:
``/NXentry/NXinstrument/NXcrystal/wavelength``
identifies a dataset called ``wavelength``
that is inside a group of type ``NXcrystal`` inside a group
of type ``NXinstrument`` inside a group of type ``NSentry``.
This nomenclature is used when the exact name of each group is
either unimportant or not specified.  Often, this will be used in
a NXDL specification to indicate the connections of a link.
