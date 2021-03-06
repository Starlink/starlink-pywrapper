

ASTELLIPSE
==========


Purpose
~~~~~~~
Create a Ellipse


Description
~~~~~~~~~~~
This application creates a new Ellipse and optionally initialises its
attributes. The Ellipse class implements a Region which represents an
ellipse within a 2-dimensional Frame.


Usage
~~~~~


::

    
       astellipse frame form centre point1 point2 unc options result
       



ADAM parameters
~~~~~~~~~~~~~~~



FMT = LITERAL (Read)
````````````````````
The format in which to store output objects. Can be "AST", "XML",
"STCS", or any FitsChan encoding such as FITS-WCS. Only used if the
output object is written to a text file. An error is reported if the
output object cannot be written using the requested format. ["AST"]



FRAME = LITERAL (Read)
``````````````````````
An NDF or text file holding the Frame in which the region is defined.
It must have exactly 2 axes. If an NDF is supplied, the current Frame
in its WCS FrameSet will be used.



FORM = _INTEGER (Read)
``````````````````````
Indicates how the ellipse is described by the remaining parameters. A
value of zero indicates that the ellipse is specified by a centre
position and two positions on the circumference. A value of one
indicates that the ellipse is specified by its centre position, the
half-lengths of its two axes, and the orientation of its first axis.



CENTRE( 2 ) = _DOUBLE (Read)
````````````````````````````
An array containing the coordinates at the centre of the ellipse.



POINT1( 2 ) = _DOUBLE (Read)
````````````````````````````
If FORM is zero, this array should contain the coordinates of one of
the four points where an axis of the ellipse crosses the circumference
of the ellipse. If FORM is one, it should contain the lengths of semi-
major and semi-minor axes of the ellipse, given as geodesic distances
within the Frame.



POINT2( 2 ) = _DOUBLE (Read)
````````````````````````````
If FORM is zero, this array should containing the coordinates at some
other point on the circumference of the ellipse, distinct from POINT1.
If FORM is one, the first element of this array should hold the angle
between the second axis of the Frame and the first ellipse axis (i.e.
the ellipse axis which is specified first in the POINT1 array), and
the second element will be ignored. The angle should be given in
radians, measured positive in the same sense as rotation from the
positive direction of the second Frame axis to the positive direction
of the first Frame axis.



OPTIONS = LITERAL (Read)
````````````````````````
A string containing an optional comma-separated list of attribute
assignments to be used for initialising the new Ellipse.



RESULT = LITERAL (Read)
```````````````````````
An text file to receive the new Ellipse.



UNC = LITERAL (Read)
````````````````````
An optional text file containing an existing Region which specifies
the uncertainties associated with each point on the boundary of the
Ellipse being created. The uncertainty at any point on the Ellipse is
found by shifting the supplied "uncertainty" Region so that it is
centred at the point being considered. The area covered by the shifted
uncertainty Region then represents the uncertainty in the position.
The uncertainty is assumed to be the same for all points.
If supplied, the uncertainty Region must be either a Box, a Circle or
an Ellipse. Alternatively, a null value (!) may be supplied, in which
case a default uncertainty is used equivalent to a box 1.0E-6 of the
size of the bounding box of the Ellipse being created.
The uncertainty Region has two uses: 1) when the astOverlap function
compares two Regions for equality the uncertainty Region is used to
determine the tolerance on the comparison, and 2) when a Region is
mapped into a different coordinate system and subsequently simplified
(using astSimplify), the uncertainties are used to determine if the
transformed boundary can be accurately represented by a specific shape
of Region.



Copyright
~~~~~~~~~
Copyright (C) 2005 Particle Physics & Astronomy Research Council. All
Rights Reserved.


Licence
~~~~~~~
This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or (at
your option) any later version.
This program is distributed in the hope that it will be useful, but
WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
General Public License for more details.
You should have received a copy of the GNU General Public License
along with this program; if not, write to the Free Software
Foundation, Inc., 51 Franklin Street,Fifth Floor, Boston, MA
02110-1301, USA


