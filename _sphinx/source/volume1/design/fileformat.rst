.. $Id$

.. _Fileformat:

=====================================
Physical File format
=====================================

.. index:: NeXus; low-level file formats
.. index:: NAPI; bypassing

This section describes how NeXus structures are mapped to features of the 
underlying physical file format.
This can also be considered a guide for people who wish to create NeXus 
files without using the NeXus-API.

.. _Fileformat-HDF-Choice:

Choice of HDF as Underlying File Format
-------------------------------------------------

.. index:: HDF
.. index:: API

At its beginnings, the founders of NeXus identified the Hierarchical Data 
Format (HDF) [#]_, as a multi-platform data storage format with capacity 
for conveying large data payloads and a substantial user community. HDF 
(now HDF5) was provided with software to read and write data (this is the 
application-programmer interface, or API) using a large number of 
computing systems in common use for neutron and X-ray science. HDF is a 
binary data file format that supports compression and structured data.

.. [#] HDF: http://www.hdfgroup.org, 
	initially from the National Center for Supercomputing 
	Applications (NCSA) at the University of Illinois at 
	Urbana-Champaign (UIUC) and later spun off into its own group
	called The HDF Group (THG).

.. _Fileformat-Mapping-HDF:

Mapping NeXus into HDF
-------------------------------------------------

.. index:: attributes

NeXus data structures map directly to HDF structures.

NeXus *groups*
	HDF4 *vgroups* or HDF5 *groups*

NeXus data sets (or *fields*)
	HDF4 *SDS (scientific data sets)* or HDF5 *datasets*

Attributes
	HDF group or dataset attributes. 

The only special case is the NeXus class name. 
HDF4 supports a group class 
which is set with the ``Vsetclass()`` call 
and read with ``VGetclass()``. 
HDF-5 has no group class. Thus the NeXus class 
is stored as a group attribute with the name ``NX_class``. 

NeXus links directly map to the HDF linking mechanisms. 



.. _Fileformat-Mapping-XML:

Mapping NeXus into XML
-------------------------------------------------

.. index:: attributes

This takes a bit more work than HDF. 
At the root of NeXus XML file 
is a XML element with the name ``NXroot``. 
Further XML attributes to 
``NXroot`` define the NeXus file level attributes.

NeXus groups are encoded into XML as elements with the name of the NeXus 
class and an XML attribute ``name`` which defines the NeXus name of the 
group. Further group attributes become XML attributes. An example of a 
NeXus group element in XML:

.. code-block:: text
	:linenos:

	<NXentry name="entry">
	</NXentry>

.. index:: dimension

NeXus data sets are encoded as XML elements with the name of the data. An 
attribute ``NAPItype`` defines the type and dimensions of the data. The 
actual data is stored as ``PCDATA`` [#]_ in the element. An example of two 
NeXus data elements in XML:

.. code-block:: text
	:linenos:

	<mode NAPItype="NX_CHAR[7]">
		monitor
	</mode>
	<counts NAPItype="NX_INT32[4]">
		21 456  127876 319
	</counts>


.. [#] ``PCDATA`` is the XML term for 
	*parsed character data* 
	(see: http://www.w3schools.com/xml/xml_cdata.asp)

.. index:: dimension
.. index:: attributes

Data are printed in appropriate formats and in C storage order. 
The codes understood for ``NAPItype`` are 
all the NeXus data type names. The dimensions
are given in square brackets as a comma 
separated list. No dimensions need to be given if 
the data is just a single value. 
Data attributes are represented as XML attributes. 
If the attribute is not a text string, then the 
attribute is given in the form: *type:value*, for example: 
``signal="NX_INT32:1"``.  

.. index:: link
.. index:: NAPIlink

NeXus links are stored in XML as XML elements with the name ``NAPIlink`` 
and a XML attribute ``target`` which stores the path to the linked entity 
in the file.  If the item is linked under a different name, then this name 
is specified as a XML attribute name to the element ``NAPIlink``. 

The authors of the NeXus API worked with the author of the miniXML XML 
[#miniXML]_ library to create a reasonably efficient way of handling 
numeric data with XML. Using the NeXus API handling something like 400 
detectors versus 2000 time channels in XML is not a problem. But you may 
hit limits with XML as the file format when data becomes to large or you 
try to process NeXus XML files with general XML tools. General XML tools 
are normally ill-prepared to process large amounts of numbers. 

.. [#miniXML] MiniXML: http://www.minixml.org/




.. _Fileformat-SpecialAttributes:

Special Attributes
-------------------------------------------------

.. index:: attributes

NeXus makes use of some special attributes for its internal purposes. 
These attributes are stored as normal group or data set attributes 
in the respective file format. These are:

.. index:: link

target
	The `target` attribute is automatically created when items get linked. 
	The target attribute contains a text string with 
	the path to the source of the item linked. 

``napimount``
	The ``napimount`` attribute is used to implement
	external linking in NeXus. 
	The string is a URL to the file and group in the 
	external file to link too. The system is meant to be extended. 
	But as of now, the only format supported is: 
	``nxfile://path-to-file#path-infile``. 
	This is a NeXus file in the file system at path-to-file 
	and the group path-infile in that 
	NeXus file.  

.. index:: NAPIlink

``NAPIlink``
	NeXus supports linking items in another group under another name. 
	This is only supported natively in HDF-5. 
	For HDF-4 and XML a crutch is needed. 
	This crutch is a special class name or attribute 
	``NAPIlink`` combined with the 
	target attribute. For groups, ``NAPILink`` 
	is the group class, for data items a special attribute 
	with the name ``NAPIlink``.  
 