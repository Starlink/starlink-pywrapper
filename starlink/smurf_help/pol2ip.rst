

POL2IP
======


Purpose
~~~~~~~
Create an Instrumental Polarisation (IP) model from a set of POL2
observations


Description
~~~~~~~~~~~
This script produces Q and U maps from a supplied list of POL2 planet
observations (this list should include observations over a wide range
of elevations). It then estimates the parameters of an IP model that
gives good estimates of the resulting Q and U, based on a supplied
total intensity map of the planet.
It is assumed that the source is centred at the reference point of the
supplied observations.
An IP model gives the normalised Q and U values (Qn and Un) with
respect to focal plane Y axis, at any point on the sky, as functions
of elevation. The correction is applied as follows:
Q_corrected = Q_original - I*Qn U_corrected = U_original - I*Un
where "I" is the total intensity at the same point on the sky as
Q_original and U_original. All (Q,U) values use the focal plane Y axis
as the reference direction.
The "PL2" IP model is as follows ("el" = elevation in radians):
p1 = A + B*el + C*el*el Qn = I*p1*cos(-2*(el-D)) Un =
I*p1*sin(-2*(el-D))
It is parameterised by four constants A, B, C and D, which are
calculated by this script. It represents an instrumental polarisation
that varies in size with elevation but is always at a fixed angle (D
radians) from the elevation axis.
The PL2 model replaces the earlier PL1 model. The difference is that
the D constant was fixed at zero in the PL1 model.


Usage
~~~~~


::

    
       pol2ip obslist iref [diam] [pixsize]
       



ADAM parameters
~~~~~~~~~~~~~~~



DIAM = _REAL (Read)
```````````````````
The diameter of the circle (in arc-seconds), centred on the source,
over which the mean Q, U and I values are found. If zero, or a
negative value, is supplied, the fit is based on the weighted mean
values within the source, where the spatial weiging function is a
fitted beam shape determined using kappa:beamfit. In this case, a text
file called "beamfit.asc" is created in the current directory. This is
a table containg columns of the geometric properties of the polarised
intensity beam in each observation. The header for this file contains
the parameters of quadratic fits to these properties, which are used
within pol2scan. [40]



ILEVEL = LITERAL (Read)
```````````````````````
Controls the level of information displayed on the screen by the
script. It can take any of the following values (note, these values
are purposefully different to the SUN/104 values to avoid confusion in
their effects):


+ "NONE": No screen output is created
+ "CRITICAL": Only critical messages are displayed such as warnings.
+ "PROGRESS": Extra messages indicating script progress are also
displayed.
+ "ATASK": Extra messages are also displayed describing each atask
invocation. Lines starting with ">>>" indicate the command name and
parameter values, and subsequent lines hold the screen output
generated by the command.
+ "DEBUG": Extra messages are also displayed containing unspecified
  debugging information. In addition scatter plots showing how each Q
  and U image compares to the mean Q and U image are displayed at this
  ILEVEL.

In adition, the glevel value can be changed by assigning a new integer
value (one of starutil.NONE, starutil.CRITICAL, starutil.PROGRESS,
starutil.ATASK or starutil.DEBUG) to the module variable
starutil.glevel. ["PROGRESS"]



IREF = NDF (Read)
`````````````````
A 2D NDF holding a map of total intensity (in pW) for the object
covered by the observations in OBSLIST. It is assumed that the object
is centred at the reference point in the map. The supplied map is
resampled to to give it the pixel size specified by parameter PIXSIZE.
If a null value(!) is supplied, the total intensity is determined from
the POL2 data itself.



LOGFILE = LITERAL (Read)
````````````````````````
The name of the log file to create if GLEVEL is not NONE. The default
is "<command>.log", where <command> is the name of the executing
script (minus any trailing ".py" suffix), and will be created in the
current directory. Any file with the same name is over-written. The
script can change the logfile if necessary by assign the new log file
path to the module variable "starutil.logfile". Any old log file will
be closed befopre the new one is opened. []



MAPDIR = LITERAL (Read)
```````````````````````
Path to a directory containing any pre-existing Q/U/I maps. Each UT
date should have a separate subdirectory within "mapdir", and each
observation should have a separate subdirectory within its <UT> date
subdirectory. Any new Q/U/I maps created by this script are placed in
this directory. If null (!) is supplied, the root directory containing
the Q/U maps is placed within the temporary directory used to store
all other intermediate files. [!]



MSG_FILTER = LITERAL (Read)
```````````````````````````
Controls the default level of information reported by Starlink atasks
invoked within the executing script. This default can be over-ridden
by including a value for the msg_filter parameter within the command
string passed to the "invoke" function. The accepted values are the
list defined in SUN/104 ("None", "Quiet", "Normal", "Verbose", etc).
["Normal"]



OBSLIST = LITERAL (Read)
````````````````````````
The path to a text file listing the POL2 observations to use. Each
line should contain a string of the form "<ut>/<obs>", where <ut> is
the 8 digit UT date (e.g. "20151009") and <obs> is the 5 digit
observation number (e.g. "00034"). Blank lines and lines starting with
"#" are ignored. The raw data for all observations is expected to
reside in a directory given by environment variable "SC2", within
subdirectories with paths of the form: $SC2/[s4a|s8a]/20150918/00056/
etc. The choice of "s8" or "s4" is made on the basis of parameter
WAVEBAND.



PIXSIZE = _REAL (Read)
``````````````````````
Pixel dimensions in the Q and U maps, in arcsec. The default is 4 arc-
sec for 850 um data and 2 arc-sec for 450 um data. []



RESTART = LITERAL (Read)
````````````````````````
If a value is assigned to this parameter, it should be the path to a
directory containing the intermediate files created by a previous run
of POL2IP (it is necessry to run POL2IP with RETAIN=YES otherwise the
directory is deleted after POL2IP terminates). If supplied, any files
which can be re-used from the supplied directory are re-used, thus
speeding things up. The path to the intermediate files can be found by
examining the log file created by the previous run. [!]



RETAIN = _LOGICAL (Read)
````````````````````````
Should the temporary directory containing the intermediate files
created by this script be retained? If not, it will be deleted before
the script exits. If retained, a message will be displayed at the end
specifying the path to the directory. [FALSE]



QUDIR = LITERAL (Read)
``````````````````````
Path to a directory containing any pre-existing Q/U/I time streams.
Each UT date should have a separate subdirectory within "qudir", and
each observation should have a separate subdirectory within its <UT>
date subdirectory. Any new Q/U/I time streams created by this script
are placed in this directory. If null (!) is supplied, the root
directory containing the Q/U time streams is placed within the
temporary directory used to store all other intermediate files. [!]



TABLE = LITERAL (Read)
``````````````````````
The path to a new text file to create in which to place a table
holding columns of elevation, Q, U, Qfit and Ufit (and various other
useful things), in TOPCAT ASCII format. [!]



TABLEIN = LITERAL (Read)
````````````````````````
The path to an existing text file containing a table created by a
previous run of this script, using the TABLE parameter. If supplied,
none of the other parameters are accessed, and a fit is performed to
the values in the supplied table. [!]



WAVEBAND = LITERAL (Read)
`````````````````````````
Indicates the waveband - "450" or "850".



Copyright
~~~~~~~~~
Copyright (C) 2015,2016 East Asian Observatory All Rights Reserved.


Licence
~~~~~~~
This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either Version 2 of the License, or (at
your option) any later version.
This program is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
General Public License for more details.
You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA
02110-1301, USA.


