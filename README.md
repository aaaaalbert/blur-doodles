# blur-doodles

How should we blur sensor values (technically, so that privacy is
protected)? How can we explain what "level of blur" achieves which
"level of privacy"? How can we further express a mapping from one
type of level to the other?

## Things to talk about
* Sensor name
* Physical unit(s), number of dimensions, sampling rate, quantization
* Privacy relevance
* Possible mitigation techniques and their properties (rate, accuracy)


### Accelerometer
Measures acceleration (m/s^2) of device in three spacial dimensions, at up to 200 Hz
(as per Android 7) and around 12 bits of nominal accuracy.

Exposes
* low-frequency audio
* user tapping on the touch screen
* LF motion (car/train/walking).
* Readings include standard gravity, and thus yield a vector indicative
  of the orientation of the device.
* Sensor exhibits device-specific noise pattern.

Rate limiting:
* Low-pass filter as desired.
* Fixed rates may still serve to undersample regular motion patterns.

Accuracy reduction:
* Round to specific precision. **How effective is this?**




### WiFi

When connected to an access point, it shows its name (SSID),
MAC address (BSSID), frequency, capabilities, RSSI, link speed;
also the device's MAC and IP addresses.

When scanning, it shows every nearby access point's SSID, BSSID,
frequency, capabilities.

Exposes
* Physical device location, as WiFi names and MAC addresses can be mapped.
* See any location-type sensor for further implications.

Rate limiting: doesn't help much, see other location-type sensors.

Accuracy reduction:
Hash and salt (keeping the salt constant across vessels
of one experiment).
