.. $Id$


.. _Introduction-DataStorageObjects:

A Set of Data Storage Objects
---------------------------------------------------------------------
.. index:: instrument definitions 

If the design principles are followed, 
it will be easy for anyone browsing a
NeXus file to understand what it contains, 
without any prior information.
However, if you are writing specialized 
visualization or analysis software, you will need to
know precisely what specific information is contained 
in advance. For that reason, NeXus
provides a way of defining the format for 
particular instrument types,
such as time-of-flight small angle neutron scattering. This requires
some agreement by the relevant communities, but enables the development of
much more portable software.

The set of data storage objects is divided into three parts:
base classes, application definitions, and contributed definitions.
The base classes represent a set of components that define 
the dictionary of all possible terms to be used with that component.
The application definitions specify the minimum required information to satisfy
a particular scientific or data analysis software interest.
The contributed definitions have been submitted by the scientific community
for incubation before they are adopted by the NIAC or for availability
to the community.

These instrument definitions are formalized as XML files, using NXDL,
(as described in the NXDL chapter in Volume II of this documentation)
to specify the names of data fields, and other NeXus data objects. 
The following is an example of such a file for
the simple NeXus file shown above. 

.. _ex.verysimple.nxdl.xml:

``verysimple.nxdl.xml``: A very simple NeXus Definition Language (NXDL) file
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: xml
	:linenos: 

	<?xml version="1.0" ?> 
	<definition 
	  xmlns="http://definition.nexusformat.org/nxdl/3.1" 
	  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	  xsi:schemaLocation="http://definition.nexusformat.org/nxdl/3.1 ../nxdl.xsd"
	  category="base"
	  name="verysimple"
	  version="1.0"
	  svnid="$Id$"
	  type="group" extends="NXobject">
	  
	  <doc>
		A very simple NeXus NXDL file
	  </doc>
	  <group type="NXentry">
		<group type="NXdata">
		  <field name="counts" type="NX_INT"  units="NX_UNITLESS">
			<doc>counts recorded by detector</doc>
		  </field>
		  <field name="two_theta" type="NX_FLOAT" units="NX_ANGLE">
			<doc>rotation angle of detector arm</doc>
		  </field>
		</group>
	  </group>
	</definition>

.. index:: example; very simple

.. (See *<link xlink:href="#Impatient">A complete example of writing and 
	reading a NeXus data file</link>* for an example to write and read data
	using the structure of :ref:`ex.verysimple.nxdl.xml`.)

This chapter has several examples of writing and reading NeXus data files.
If you want to define the format of a particular type of NeXus file
for your own use, e.g. as the standard output from a program, you are encouraged
to *publish* the format using this XML format. 
An example of how to do this is shown in the section titled
Creating a NXDL Specification (:ref:`NXDL_Tutorial-CreatingNxdlSpec`).
