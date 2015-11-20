.. $Id$

.. _DataRules:

Rules for Storing Data Items in NeXus Files
===========================================

This section describes the rules which apply for 
storing single data fields in data files.



.. _Design-Naming:

Naming Conventions
------------------

Group and field names used within NeXus follow a naming 
convention which adheres to these rules. :index:`rules; naming`
The names of NeXus `group <Design-Groups>`_ and `field <Design-Fields>`_ 
objects must contain only a restricted set of characters.
This set may be described by this regular expression syntax.

.. _RegExpName:

::

    [A-Za-z_][\w_]*

This name pattern starts with a letter (upper or lower case)
or "`_`" (underscore), then letters, 
numbers, and "`_`" and is limited to no more than 63 characters
(imposed by the HDF5 rules for names). 

.. index:: rules; HDF5

Sometimes it is necessary to combine words in order to
build a descriptive name for a data field or a group. 
In such cases lowercase words are connected by underscores. ::

            number_of_lenses

For all data fields, only names from the NeXus base class dictionaries are to 
be used.
If a data field name or even a complete component is missing, 
please suggest the addition to the NIAC. The addition will usually be 
accepted provided it is adequately documented
and not a duplication of an existing field. 

.. note:
   The NeXus base classes provide a comprehensive dictionary
   of terms than can be used for each class. 
   :index:`NeXus basic motivation; defined dictionary`



.. _Design-NeXusDimensions:

NeXus Storage
-------------

NeXus stores multi dimensional arrays of physical values 
in C language storage order, :index:`dimension; storage order`
last dimension is the fastest varying. This is the rule. 

   **Good reasons are required to deviate from this rule.**

One good reason to deviate from this rule is the situation 
where data must be streamed to disk as fast as possible and 
a conversion to NeXus storage order is not possible. 
In such cases, exceptions can be made. It is possible 
to store data in other storage orders in NeXus 
as well as to specify that the data needs to be converted first 
before being useful. 

.. ... store data in other storage orders in NeXus ...
   <!-- TODO What does this say?  Compound thoughts? --> 



.. _Design-NonCStorageOrder:

Non C Storage Order
...................

In order to indicate that the storage order :index:`dimension; storage order`
is different from C storage order two
additional data set attributes, offset and stride, 
have to be stored which together define the storage 
layout of the data. Offset and stride contain rank 
numbers according to the rank of the multidimensional 
data set. Offset describes the step to make when the 
dimension is multiplied by 1. Stride defines the step to 
make when incrementing the dimension. 
This is best explained by some examples.  	   


Offset and Stride for 1-D data
++++++++++++++++++++++++++++++

* raw data = 0 1 2 3 4 5 6 7 8 9

.. code-block:: text
	
	size[1] = { 10 }  // assume uniform overall array dimensions

* default stride

.. code-block:: text
	:linenos:
	
	stride[1] = { 1 }
	offset[1] = { 0 }
	for i:
         result[i]:
            0 1 2 3 4 5 6 7 8 9

* reverse stride

.. code-block:: text
	:linenos:
	
	stride[1] = { -1 }
	offset[1] = { 9 }
	for i:
	     result[i]:
	        9 8 7 6 5 4 3 2 1 0	   


Offset and Stride for 2-D data
++++++++++++++++++++++++++++++

* raw data = 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19

.. code-block:: text
	
	size[2] = { 4, 5 }  // assume uniform overall array dimensions

* row major (C) stride

.. code-block:: text
	:linenos:
	
	stride[2] = { 5, 1 }
	offset[2] = { 0, 0 }
	for i:
	     for j:
	        result[i][j]:
	           0 1 2 3 4
	           5 6 7 8 9
	           10 11 12 13 14
	           15 16 17 18 19

* column major (Fortran) stride

.. code-block:: text
	:linenos:
	
	stride[2] = { 1, 4 }
	offset[2] = { 0, 0 }
	for i:
	     for j:
	        result[i][j]:
	           0 4 8 12 16
	           1 5 9 13 17
	           2 6 10 14 18
	           3 7 11 15 19

* "crazy reverse" row major (C) stride

.. code-block:: text
	:linenos:
	
	stride[2] = { -5, -1 }
	offset[2] = { 4, 5 }
	for i:
	     for j:
	        result[i][j]:
	           19 18 17 16 15
	           14 13 12 11 10
	           9 8 7 6 5
	           4 3 2 1 0   	   


Offset and Stride for 3-D data
++++++++++++++++++++++++++++++

* raw data = 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19
  20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37 38 39
  40 41 42 43 44 45 46 47 48 49 50 51 52 53 54 55 56 57 58 59

.. code-block:: text
	
	size[3] = { 3, 4, 5 }  // assume uniform overall array dimensions

* row major (C) stride

.. code-block:: text
	:linenos:

	stride[3] = { 20, 5, 1 }
	offset[3] = { 0, 0, 0 }
	for i:
	     for j:
	        for k:
	           result[i][j][k]:
	              0 1 2 3 4
	              5 6 7 8 9
	              10 11 12 13 14
	              15 16 17 18 19
	
	              20 21 22 23 24
	              25 26 27 28 29
	              30 31 32 33 34
	              35 36 37 38 39
	
	              40 41 42 43 44
	              45 46 47 48 49
	              50 51 52 53 54
	              55 56 57 58 59

* column major (Fortran) stride

.. code-block:: text
	:linenos:
	
	stride[3] = { 1, 3, 12 }
	offset[3] = { 0, 0, 0 }
	for i:
	     for j:
	        for k:
	           result[i][j][k]:
	              0 12 24 36 48
	              3 15 27 39 51
	              6 18 30 42 54
	              9 21 33 45 57
	
	              1 13 25 37 49
	              4 16 28 40 52
	              7 19 31 43 55
	              10 22 34 46 58
	
	              2 14 26 38 50
	              5 17 29 41 53
	              8 20 32 44 56
	              11 23 35 47 59 

.. 2011-10-15,PRJ:  NXformula has not been ratified by the NIAC.  
   This entire part is premature.

   .. _Design-DataValueTransformations:
   
   Data Value Transformations
   ++++++++++++++++++++++++++
   
   .. TODO: Is it too early to include a section about Data Value Transformations and NXformula?
    
   It is possible to store raw values in NeXus data files. Such data has to be stored in 
   special `NXformula` [#]_ groups together with the data and information required to transform
   it into physical values. 
   
   .. [#] NeXus has not yet defined the `NXformula` group (or base class) for use in NeXus data files.
          The exact content of the `NXformula` group is still under discussion.



.. _Design-DataTypes:

NeXus Data Types
----------------

Matching regular expressions for NeXus data types

================  ===================================
description       matching regular expression
================  ===================================
integer           ``NX_INT(8|16|32|64)``
floating-point    ``NX_FLOAT(32|64)``
array             ``(\[0-9\])?``
valid item name   ``^[A-Za-z_][A-Za-z0-9_]*$``
valid class name  ``^NX[A-Za-z0-9_]*$``
================  ===================================

NeXus supports numeric data as either integer or floating-point
numbers.  A number follows that indicates the number of bits in the word.
The table above shows the regular expressions that
matches the data type specifier.

integers
    ``NX_INT8``, ``NX_INT16``, ``NX_INT32``, or ``NX_INT64``

floating-point numbers
    ``NX_FLOAT32`` or ``NX_FLOAT64``

date / time stamps
    ``NX_DATE_TIME`` or ``ISO8601``
 	
    Dates and times :index:`date and time` are specified using
    ISO-8601 standard definitions.
    Refer to :ref:`Design-Dates-Times`.

strings
    All strings are to be encoded in UTF-8. Since most strings in a
    NeXus file are restricted to a small set of characters and 
    the first 128 characters are standard across encodings,
    the encoding of most of the strings in a NeXus file will be a moot point.
    UTF-8 encoding will be important when recording 
    peoples' names in :ref:`NXuser`
    and text notes in :ref:`NXnote`.
    
    .. index:: utility; nxvalidate

    Because the few places where encoding is important also 
    have unpredictable content, as well as the way in which
    current operating systems handle character encoding, it 
    is practically impossible to test the encoding used. Hence,
    `nxvalidate` provides no messages relating to character encoding.

binary data
    Binary data is to be written as ``UINT8``.

images
    Binary image data is to be written using ``UINT8``, 
    the same as binary data, but with an accompanying image mime-type.
    If the data is text, the line terminator is ``[CR][LF]``.



.. _Design-Dates-Times:

NeXus dates and times
---------------------

.. index:: date and time

NeXus dates and times should be stored using the 
ISO 8601 [#ISO8601]_ format, such as:

.. code-block:: text

	1996-07-31T21:15:22+0600

**Note:**
     The `T` appears literally in the string, 
     to indicate the beginning of the time element, as specified 
     in ISO 8601.  It is common to use a space in place of the `T`.
     While human-readable, compatibility with the ISO 8601 standard is not 
     assured with this substitution. 

The standard also allows for time intervals in fractional seconds
with *1 or more digits of precision*.
This avoids confusion, e.g. between U.S. and European conventions, 
and is appropriate for machine sorting. 

.. [#ISO8601] ISO 8601, http://www.w3.org/TR/NOTE-datetime

.. Uh, a leftover ...    </section>   ... something above should be one level lower.




.. _Design-Units:

NeXus Units
-----------

.. index:: units

Given the plethora of possible applications of NeXus, it is difficult to 
define units 
to use. Therefore, the general rule is that you are free to 
store data in any unit you find fit. However, any data field must have a 
units attribute which describes the units, Wherever possible, SI units are 
preferred. NeXus units are written as a string attribute (``NX_CHAR``) 
and describe the engineering units. The string
should be appropriate for the value. 
Values for the NeXus units must be specified in
a format compatible with Unidata UDunits. [#UDunits]_
The UDunits specification also includes instructions  for derived units.
At present, the contents of NeXus `units` attributes
are not validated in data files.
Application definitions may specify units to be used for fields 
using an  `enumeration`. :index:`enumeration`

.. [#UDunits] Unidata UDunits, http://www.unidata.ucar.edu/software/udunits/udunits-2-units.html


Linking Multi Dimensional Data with Axis Data
---------------------------------------------

NeXus allows to store multi dimensional arrays of data.
In most cases 
it is not sufficient to just have the indices into the array as a label for 
the dimensions of the data. Usually the information which physical value 
corresponds to an index into a dimension :index:`dimension`
of the multi dimensional data set.
To this purpose a means is needed to locate appropriate data arrays which describe 
what each dimension of a multi dimensional data set actually corresponds too. 
There is a standard HDF facility to do this: it is called dimension scales. 
Unfortunately, at a time, there was only one global namespace for dimension scales.
Thus NeXus had to come up with its own scheme for locating axis data which is described 
here. A side effect of the NeXus scheme is that it is possible to have multiple 
mappings of a given dimension to physical data. For example a TOF data set can have the TOF 
dimension as raw TOF or as energy. 
       
There are two methods of linking :index:`link`
each data dimension to its respective dimension scale. 
:index:`dimension; dimension scales`
The preferred method uses the ``axes`` attribute
to specify the names of each dimension scale.
The original method uses the ``axis`` attribute to identify
with an integer the axis whose value is the number of the dimension.
After describing each of these methods, the two methods will be compared.
A prerequisite for both methods is that the data fields describing the axis 
are stored together with the multi dimensional data set whose axes need to be defined 
in the same NeXus group. If this leads to data duplication, use links.  



.. _Design-Linking-ByName:

Linking by name using the `axes` attribute
..........................................
            
The preferred method is to define an attribute of the data itself
called *axes*. :index:`axes`  The ``axes`` attribute contains the names of 
each dimension scale :index:`dimension; dimension scales`
as a colon (or comma) separated list in 
the order they appear in C.  For example: 

Preferred way of denoting axes
++++++++++++++++++++++++++++++


.. code-block:: text
	:linenos:

	data:NXdata
	    time_of_flight = 1500.0 1502.0 1504.0 ...
	    polar_angle = 15.0 15.6 16.2 ...
	    some_other_angle = 0.0 0.0 2.0 ...
	    data = 5 7 14 ...
	      @axes = polar_angle:time_of_flight
	      @signal = 1



.. _Design-LinkingByDimNumber:

Linking by dimension number using the `axis` attribute
++++++++++++++++++++++++++++++++++++++++++++++++++++++

The original method is to define an attribute of each dimension
scale called *axis*. :index:`axis`
It is an integer whose value is the number of
the dimension, in order of fastest varying dimension. :index:`dimension; fastest varying`
That is, if the array being stored is data with elements
``data[j][i]`` in C and
``data(i,j)`` in Fortran, where ``i`` is the 
time-of-flight index and ``j`` is
the polar angle index, the :ref:`NXdata` group :index:`NXdata`
would contain:

.. code-block:: text
	:linenos:

	data:NXdata
	    time_of_flight = 1500.0 1502.0 1504.0 ...
	      @axis = 1
	      @primary = 1
	    polar_angle = 15.0 15.6 16.2 ...
	      @axis = 2
	      @primary = 1
	    some_other_angle = 0.0 0.0 2.0 ...
	      @axis = 1
	    data = 5 7 14 ...
	      @signal = 1

The ``axis`` attribute must 
be defined for each dimension scale.
The ``primary`` attribute is unique to this method of linking.

There are limited circumstances in which more 
than one dimension scale :index:`dimension; dimension scales`
for the same data dimension can be included in the same 
:ref:`NXdata` group. :index:`NXdata`
The most common is when the dimension scales are 
the three components of an 
*(hkl)* scan. In order to
handle this case, we have defined another attribute 
of type integer called
``primary`` whose value determines the order 
in which the scale is expected to be
chosen for plotting, :index:`NeXus basic motivation; default plot`
i.e.

   **Note:**	      
   The `primary` attribute can only be 
   used with the first method of defining dimension scales 
   :index:`dimension; dimension scales`
   discussed above. In addition to 
   the ``signal`` data, this
   group could contain a data set of the same rank
   :index:`rank`
   and dimensions called ``errors``
   containing the standard deviations of the data.

1st choice:
   ``primary="1"``

2nd choice:
   ``primary="2"``

etc.

If there is more than one scale with the same value of the ``axis`` attribute, one
of them must have set ``primary="1"``. Defining the ``primary``
attribute for the other scales is optional.


.. _Design-Linking-Discussion:

Discussion of the two linking methods
+++++++++++++++++++++++++++++++++++++

In general the method using the ``axes`` attribute on the multi dimensional 
data set :index:`dimension; data set` should be preferred. 
This leaves the actual axis describing data sets
unannotated and allows them to be used as an axis for other multi dimensional
data.  This is especially a concern as an axis describing a data set may be linked 
into another group where it may describe a completely different dimension
of another data set. 

Only when alternative axes definitions are needed, the ``axis`` method 
should be used to specify an axis of a data set.  
This is shown in the example above for 
the ``some_other_angle`` field where ``axis="1"``
denotes another possible primary axis for plotting.  The default
axis for plotting carries the ``primary="1"`` attribute.

Both methods of linking data axes will be supported in NeXus
utilities that identify dimension scales, :index:`dimension; dimension scales`
such as ``NXUfindaxis()``.


.. _Rules-StoringDetectors:

Storing Detectors
-----------------

There are very different types of detectors out there. Storing their data 
can be a challenge. As a general guide line: if the detector has some 
well defined form, this should be reflected in the data file. A linear 
detector becomes a linear array, a rectangular detector becomes an 
array of size ``xsize`` times ``ysize``. 
Some detectors are so irregular that this 
does not work. Then the detector data is stored as a linear array, with the
index being detector number till ``ndet``. Such detectors must be accompanied
by further arrays of length ``ndet`` which give 
``azimuthal_angle``, ``polar_angle`` and ``distance`` for each detector. 

If data from a time of flight (TOF) instrument must be described, then the 
TOF dimension becomes the last dimension, for example an area detector of 
``xsize`` *vs.* ``ysize`` 
is stored with TOF as an array with dimensions 
``xsize``, ``ysize``, ``ntof``.


.. _Rules-StoringData-Monitors:

Monitors are Special
--------------------

Monitors, :index:`monitor` detectors that measure the properties 
of the experimental probe rather than the 
sample, have a special place in NeXus files. Monitors are crucial to normalize data.
To emphasize their role, monitors are not stored in the 
:ref:`NXinstrument` hierarchy but as :ref:`NXmonitor` group(s) as direct
children of the :ref:`NXentry` level, as there might be multiple monitors. Of special 
importance is the monitor in a group called ``control``. 
This is the main monitor against which the data has to be normalized. 
This group also contains the counting control information, 
i.e. counting mode, times, etc.

Monitor data may be multidimensional. Good examples are scan monitors 
where a monitor value per scan point is expected or 
time-of-flight monitors.
