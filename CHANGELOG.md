1.0.1 (2013-03-22)
------------------
* Added method to turn off the LED entirely.
* Fixed method errors for `Device.set_led`.
* Fixed bug preventing orange LED from being set (was not using the
  orange-specific brightness of `0x04`, a constraint not present for other
  colors; but makes perfect sense given voltage, etc).
* Fixed bug preventing LED being set to full brightness in some cases by using
  `0x0f` instead of `0x10` for `MAX_BRIGHTNESS`.
* Give the device a quarter-second to report back after sending LED state
  commands, so the buffer doesn't get polluted with the response next time we
  try to open the device (though the long-term fix here is a read until we
  start getting measurement records, if I'm not mistaken)


1.0.0 (2013-03-22)
------------------
* Initial release on GitHub and PyPI. Sets LED color, brightness, and provides
  temperature readings.
