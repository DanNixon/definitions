.. $Id$


.. _FAQ:

==========================
Frequently Asked Questions
==========================

.. Undefined Labels
   ----------------

.. _this example:
.. _mailing lists:
.. _nexus api:
.. _definitions repository:
.. _nxvalidate-java:


.. index:: FAQ

This is a list of commonly asked questions concerning the NeXus data format.


How many facilities use NeXus?
-----------------------------------------------------------

This is not easy to say, not all facilities using NeXus actively
participate in the committee. Some facilities (the list is incomplete) 
have reported their adoption status on the NeXus wiki [#]_.
Please have a look at this list.

    .. [#] Facilities reporting use of NeXus:  http://wiki.nexusformat.org/Facilities

NeXus files are binary? This is crazy! How am I supposed to see my data?
---------------------------------------------------------------------------


NeXus files are not binary *per se*. If you use the XML backend the
data are stored in a relatively human readable form (see
:ref:`this example`).
This backend however is only recommended for very small data sets. With
the multidimensional data that is routinely recorded on many modern
instruments it is very difficult anyway to retrieve useful
information on a VT100 terminal. If you want to try, for example
``nxbrowse``
is a utility provided by the NeXus community that can be very
helpful to those who want to inspect their files and avoid
graphical applications. For larger data volumes the binary backends
used with the appropriate tools are by far superior in terms of
efficiency and speed and most users happily accept that after having
worked with supersized "human readable" files for a while.

What on-disk file format should I choose for my data?
---------------------------------------------------------------------------

HDF5 is the default file container to use for NeXus data. It
is the recommended format for all applications. HDF4 is still
supported as a on disk format for NeXus but for new installations
preference should be given to HDF5. The XML backend is available
for special use cases. Choose this option with care considering the
space and speed implications.

Why are the NeXus classes so complicated? I'll never store all that information
--------------------------------------------------------------------------------------

The NeXus classes are essentially *glossaries of terms*. If you
need to store a piece of information, consult the class definitions
to see if it has been defined. If so, use it. It is not compulsory
to include every item that has been defined in the base class if it
is not relevant to your experiment. On the other hand, a NeXus
application definition lists a smaller set of compulsory items that
should allow other researchers or software to analyze your data.
You should really follow the application definition that
corresponds to your experiment to take full advantage of NeXus.

I don't like NeXus. It seems much faster and simpler to develop my own file format. Why should I even consider NeXus?
------------------------------------------------------------------------------------------------------------------------------------------------------

If you consider using an efficient on disk storage format,
HDF5 is a better choice than most others. It is fast and efficient
and well supported in all main stream programming languages and a
fair share of popular analysis packages. The format is so widely
used and backed by a big organisation that it will continue to be
supported for the foreseeable future.
So if you are going to use HDF5 anyway, why not use the NeXus
definition to lay out the data in a standardised way? The NeXus
community spent years trying to get the standard right and
while you will not agree with every single choice they made in the
past, you should be able to store the data you have in a quite
reasonable way. If you do not comply with NeXus chances are most
people will perceive your format as different but not necessarily
better than NeXus by any large measure. So it may not be worth the
effort. Seriously.
If you encounter any problems because the classes are not
sufficient to describe your configuration, please contact the NIAC
Executive Secretary explaining the problem, and post a suggestion
at the relevant class wiki page. Or raise the problem in one of the
:ref:`mailing lists`.
The NIAC is always willing to consider new proposals.

.. index:: NIAC

I want to produce an application definition. How do I go about it?
---------------------------------------------------------------------------

.. index:: NXDL

Read the NXDL Tutorial in
:ref:`NXDL_Tutorial-CreatingNxdlSpec`.
The procedures for acceptance are defined in the NIAC constitution.
Refer to the most recent version of the NIAC constitution on the
NIAC wiki [#]_.

    .. [#] NIAC wiki: http://www.nexusformat.org/NIAC

What is the purpose of ``NXdata``?
---------------------------------------------------------------------------

.. index:: NeXus basic motivation; default plot

``NXdata`` contains links to the data stored elsewhere in the
``NXentry``. It identifies the default plottable data. This is one of the
basic motivations (see :ref:`SimplePlotting`)
for the NeXus standard. The choice of the name ``NXdata``
is historic and does not really reflect its function.


.. _`how to find the plottable data`:

How do I identify the plottable data?
---------------------------------------------------------------------------

.. index:: NeXus basic motivation; default plot

Any program whose aim is to identify plottable data should use the
following procedure:
  
  .. index:: dimension scale
  .. index:: rank

#. Open the first top level NeXus group with class ``NXentry``.
#. Open the first NeXus group with class ``NXdata``.
#. Loop through NeXus fields in this group searching for the item
   with attribute ``signal="1"``
   indicating this field has the plottable data.
#. Check to see if this field has an attribute called
   ``axes``. If so, the attribute value contains a colon (or comma)
   delimited list (in the C-order of the data array) with the names
   of the dimension scales
   associated with the plottable data. And
   then you can skip the next two steps.      
#. If the ``axes``
   attribute is not defined, search for the one-dimensional NeXus
   fields with attribute ``primary="1"``.
#. These are the dimension scales
   to label the axes of each
   dimension of the data.
#. Link each dimension scale
   to the respective data dimension by
   the ``axis`` attribute (``axis="1"``,
   ``axis="2"``, ... up to the rank of the data).
#. If necessary, close the ``NXdata``
   group, open the next one and repeat steps 3 to 6.
#. If necessary, close the ``NXentry``
   group, open the next one and repeat steps 2 to 7.

Consult the :ref:`NeXus API`
section, which describes the routines available to program these
operations. In the course of time, generic NeXus browsers will
provide this functionality automatically.


How can I specify reasonable axes for my data?
---------------------------------------------------------------------------

See the section: :ref:`NXdata-facilitates-TheDefaultPlot`.

Why aren't ``NXsample`` and ``NXmonitor`` groups stored in the ``NXinstrument`` group?
------------------------------------------------------------------------------------------------

A NeXus file can contain a number of ``NXentry``
groups, which may represent different scans in an experiment, or
sample and calibration runs, etc. In many cases, though by no means
all, the instrument has the same configuration so that it would be
possible to save space by storing the ``NXinstrument``
group once and using multiple links in the remaining ``NXentry``
groups. It is assumed that the sample and monitor information would
be more likely to change from run to run, and so should be stored
at the top level.

Specifications are boring. Where can I find some good example data files?
---------------------------------------------------------------------------

There are a few checked into the :ref:`definitions repository`.
At the moment the selection is quite limited and not very representative.

Can I use a NXDL specification to parse a NeXus data file?
---------------------------------------------------------------------------

This should be possible as there is nothing in the NeXus
specifications to prevent this but it is not implemented in NAPI.
You would need to implement it for yourself. You would be wise to
consult the algorithms in the Java version of
``NXvalidate``
(see :ref:`NXvalidate-java`) for more details.

Why do I need to specify the ``NAPItype``? 
--------------------------------------------

*My programming language does not need that information and 
I don't care about C and colleagues. Can I leave it out?*

.. index:: NAPI

``NAPItype``
is necessary. When implementing the NeXus-XML API we strived to
make this as general as HDF and reasonably efficient for medium
sized datasets. This is why we store arrays as a large bunch of
numbers in C-storage order. And we need the
``NAPItype``
to figure out the dimensions of the dataset.

.. index:: dimension; data set

Do I have to use the ``NAPI`` subroutines? Can't I read (or write) the NeXus data files with my own routines?
------------------------------------------------------------------------------------------------------------------------------------------------------

You are not required to use the NAPI to write valid NeXus
data files. It is possible to avoid the NAPI to write and read
valid NeXus data files. But, the programmer who chooses this path
must have more understanding of how the NeXus HDF or XML data file
is written. Validation of data files written without the NAPI is
strongly encouraged.

I'm using links to place data in two places. Which one should be the data and which one is the link?
------------------------------------------------------------------------------------------------------------------------------------------------------

.. COMMENT: say it clearly
.. COMMENT: answer the question
.. COMMENT: say it again another way

NeXus uses HDF5 hard links.
Both places have pointers to the actual data.
That is the way hard links work in HDF5.
There is no need for a preference to either location.
NeXus defines a ``target`` attribute to label
one directory entry as the source of the data (in this, the
link *target*).  This has value in
only a few situations such as when
converting the data from one format to another.  By identifying
the original in place, duplicate copies of the data are not
converted.
In HDF, a hard link points to a data object.
A soft link points to a directory entry.
Since NeXus uses hard links, there is no need to distinguish
between two (or more) directory entries that point to the same data.

.. index:: link
