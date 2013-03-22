gotemp
======

This is a Python module to interact with GoTemp! temperature sensors. The
module provides capabilities to obtain a single reading from the device, and to
manipulate the color and brightness of its built-in LED.

Installation
------------

The gentle reader will want to have been installing from pypi:

`pip install gotemp`

Usage
-----

The `Device` class can be used easily in the context of a `with` statement, or
as an independent instance. The following two examples, then, which poll for
the temperature and run a brief LED test, are equivalent:

```python
import gotemp

with gotemp.Device('/dev/ldusb0') as sensor:
    deg_c, deg_f = sensor.get_reading()
    sensor.test_leds()

print '%0.2f degrees C, %0.2f degrees F' % (deg_c, deg_f)
```

```python
import gotemp

sensor = gotemp.Device('/dev/ldusb0')
sensor.open()

deg_c, deg_f = sensor.get_reading()
sensor.test_leds()

sensor.close()

print '%0.2f degrees C, %0.2f degrees F' % (deg_c, deg_f)
```

Real Examples
-------------

I currently use this library to log temperatures to a file every minute on a
server, which then gets picked up, parsed, and sent to Graphite for archival
and pretty graphs:

```python
import time
import gotemp
from os import getenv

usb_dev = getenv('USB_DEVICE', '/dev/ldusb0')
with gotemp.Device(usb_dev) as sensor:
    deg_c, deg_f = sensor.get_reading()

print '%0.5f|%0.5f|%0.5f' % (time.time(), deg_c, deg_f)
```

Special Thanks
--------------

This couldn't have been done without community contributions from these lovely
folks:

* The Herd Of Kittens' `gotemp-ldusb.py` utility (2008)
  (http://www.thok.org/intranet/python/vernier/README.html)
* Scott Tsai's `gotemp-lights.py` utility (2010)
  (https://gitorious.org/scottt/gotemp)

License
-------

Copyright (c) 2013, Brian Cline.
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this
  list of conditions and the following disclaimer.
* Redistributions in binary form must reproduce the above copyright notice,
  this list of conditions and the following disclaimer in the documentation
  and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
