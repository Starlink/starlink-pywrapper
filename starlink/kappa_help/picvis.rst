

PICVIS
======


Purpose
~~~~~~~
Finds the first unobscured FRAME picture in the graphics database


Description
~~~~~~~~~~~
This application selects the first, i.e. oldest, unobstructed FRAME
picture in the graphics database for a graphics device. Unobstructed
means that there is no younger picture overlying it either wholly or
in part.


Usage
~~~~~


::

    
       picvis [device]
       



ADAM parameters
~~~~~~~~~~~~~~~



DEVICE = DEVICE (Read)
``````````````````````
The graphics workstation. [The current graphics device]



Examples
~~~~~~~~
picvis
This selects the first unobscured FRAME picture for the current
graphics device.
picvis xwindows
This selects the first unobscured FRAME picture for the xwindows
graphics device.



Notes
~~~~~


+ An error is returned if there is no unobscured FRAME picture, and
the current picture remains unchanged.
+ This routine cannot know whether or a picture has been cleared, and
  hence is safe to reuse, as such information is not stored in the
  graphics database.




Related Applications
~~~~~~~~~~~~~~~~~~~~
KAPPA: PICEMPTY, PICENTIRE, PICGRID, PICLAST, PICLIST, PICSEL.


Timing
~~~~~~
The execution time is approximately proportional to a linear
combination of the number of pictures in the database before the
unobstructed FRAME picture is found, and the square of the number of
pictures in the database.


Copyright
~~~~~~~~~
Copyright (C) 1995, 2004 Central Laboratory of the Research Councils.
All Rights Reserved.


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


