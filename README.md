# blur-doodles

How should we blur sensor values (technically, so that privacy is
protected)? How can we explain what "level of blur" achieves which
"level of privacy"? How can we further express a mapping from one
type of level to the other?

## Things to talk about
* Sensor and physical unit (...) measured
* Privacy relevance
* Possible rate and accuracy mitigation techniques and their properties


### Accelerometer
Measures acceleration (m/s^2) of device in three spacial dimensions, at up to 200 Hz
(as per Android 7) and around 12 bits of nominal accuracy.

Exposes low-frequency audio, user tapping on the touch screen,
LF motion (car/train/walking).

Readings include standard gravity, and thus yield a normal vector indicative
of the orientation of the device.

Also, sensor exhibits device-specific noise pattern.

Rate: low-pass filter as desired. (Fixed rates may still serve to
undersample regular motion patterns.)

Accuracy: Round to specific precision. **How effective is this?**


### WiFi

